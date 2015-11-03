# Introduction #

Django is one of the best web frameworks in python. Quite often portals and CRM systems are built on Django and in this example we are integrating a customer portal with Tryton.

The features would be:
  1. See Invoices online
  1. View detailed invoice

# Details #

Lets assume that the django app that needs to use tryton is `accounts`

---

my\_site/<br />
> init.py<br />
> settings.py<br />
> urls.py<br />
> accounts/<br />
> > init.py<br />
> > models.py<br />
> > tryton.py<br />
> > views.py<br />

> templates/<br />
> > my\_invoices\_template.html<br />
> > invoice\_detail.html<br />


---

## Step 1:Relating a login account to a party ##

It is necessary to know the party ID of the user who has logged into the portal. This information can be stored in the user profile. The recommended way of storing additional information of a user in django is by the use of AUTH\_PROFILE\_MODULE See http://docs.djangoproject.com/en/dev/topics/auth/#storing-additional-information-about-users for details.

In this case we call the profile module as `AuthProfile`

create a new Profile class in your models.py:

```
from django.db import models

class AuthProfile(models.Model):
    tryton_id = models.IntegerField(
        null=True,
        blank=True,
    )
```

To get the tryton ID of the current user we can use `User.get_profile().tryton_id`

## Step 2:Setting up django to use tryton ##

Accessing tryton has a module needs you to pass credentials. To make your code as generic as possible it is advised to store these settings in the settings.py file of Django.

Here is an example:

```
ENABLE_TRYTON = True
TRYTOND_PATH = '/usr/local/tryton/trytond/'
TRYTON_UN = 'apiuser'
TRYTON_PW = 'apipass'
TRYTON_DB = 'open'
```

Building a wrapper to access Tryton as a module

Ceate a file tryton.py in your `accounts` app
```
from django.conf import settings
import sys, os
import warnings
warnings.filterwarnings("ignore", message="Old style callback, usecb_func(ok, store) instead")

TRYTOND_PATH = settings.TRYTOND_PATH

DIR = os.path.abspath(os.path.normpath(os.path.join(TRYTOND_PATH,'trytond')))
if os.path.isdir(DIR):
    sys.path.insert(0, os.path.dirname(DIR))

from trytond.modules import register_classes
from trytond.pool import Pool
from trytond.backend import Database
from trytond.tools import Cache

# Register classes populates the pool of models:
register_classes()

# Instantiate the database and the pool
DB = Database(settings.TRYTON_DB).connect()
POOL = Pool(settings.TRYTON_DB)
POOL.init()
user_obj = POOL.get('res.user')
cursor = DB.cursor()
Cache.clean(settings.TRYTON_DB)
try:
    # User 0 is root user. We use it to get the user id:
    USER = user_obj.search(cursor, 0, [
            ('login', '=', settings.TRYTON_UN),
            ], limit=1)[0]
finally:
    cursor.close()
    Cache.resets(settings.TRYTON_DB)
```

## Step 3:Using Tryton in the view ##

Lets assume that we need two views:
  1. For List of invoices
  1. Details of invoices
available at the URLs `/accounts/invoices/` and `/accounts/invoices/<invno>/` and a final download url at `/accounts/invoices/<invno>/download`

The urls.py settings would be:
```
(r'^accounts/invoices/(\d+)/download$', 'accounts.views.download_invoice'),
(r'^accounts/invoices/(\d+)/$', 'accounts.views.view_invoice_detail'),
(r'^accounts/invoices/$', 'accounts.views.view_invoices'),
```

To display the Invoices of the party lets write a custom view.

```
from django.shortcuts import render_to_response

def view_invoices(request):
    context = {}
    try:
        party_id = request.user.get_profile().tryton_id
    except:
        party_id = False
    if settings.ENABLE_TRYTON and party_id:
        from tryton import POOL, DB, USER
        from trytond.tools import Cache
        invoice_obj = POOL.get('account.invoice')
        cursor = DB.cursor()
        Cache.clean(POOL.database_name)
        try:
            invoice_ids = invoice_obj.search(cursor, USER, [('party', '=', party_id)])
            context['invoices'] = invoice_obj.browse(cursor, USER, invoice_ids)
            return render_to_response('my_invoices_template.html', context)
        finally:
	    cursor.commit()
            Cache.resets(POOL.database_name)
    return render_to_response('my_invoices_template.html', context)
```

And a simple template for `my_invoices_template.html` would be:

```
{% if invoices %}
<table border="1" cellpadding="2" cellspacing="0" width="100%">
  <tr>
    <th>Date</th>
    <th>Invoice No [Reference]</th>
    <th>Description</th>
    <th>Untaxed</th>
    <th>Tax</th>
    <th>Total</th>
    <th>Amount Due</th>
    <th>Currency</th>
    <th>State</th>
  </tr>
  {% for each in invoices %}
  <tr>
    <td><a href="/accounts/invoices/{{each.id}}/">{{each.invoice_date}}</a></td>
    <td><a href="/accounts/invoices/{{each.id}}/"><b>{{each.number}}</b> 
{%if each.reference%}
[{{each.reference}}] 
{% endif %}</a></td>
    <td><a href="/accounts/invoices/{{each.id}}/">{{each.description}}</a></td>
    <td>{{each.untaxed_amount}}</td>
    <td>{{each.tax_amount}}</td>
    <td>{{each.total_amount}}</td>
    <td>{{each.amount_to_pay}}</td>
    <td>{{each.currency.code}}</td>
    <td>{{each.state}}</td>
  </tr>
  {% endfor %}
</table>
{% else %}
<h4>You do not have any invoices in your account.</h4>
{% endif %}
```

Now over to the detailed view:

The view code would be:
```
from django.shortcuts import render_to_response

def view_invoice_detail(request, inv_id):
    inv_id = int(inv_id)
    context = {}
    try:
        party_id = request.user.get_profile().tryton_id
    except:
        party_id = False
    if settings.ENABLE_TRYTON and party_id:
        from tryton import POOL, DB, USER
        from trytond.tools import Cache
        try:
            cursor = DB.cursor()
            Cache.clean(POOL.database_name)
            invoice_obj = POOL.get('account.invoice')
            invoice = invoice_obj.browse(cursor, USER, inv_id)
            context['invoice'] = invoice
            return render_to_response('invoice_detail.html', context)
        finally:
    	    cursor.commit()
            Cache.resets(POOL.database_name)
    return render_to_response('invoice_detail.html', context)
```

And a simple template of `invoice_detail.html`:

```
{% if invoice %}
<table border="1" cellpadding="2" cellspacing="0" width="100%">
	<tr>
		<td>Invoice Date:</td>
		<td>{{invoice.invoice_date}}</td>
	</tr>
	<tr>
		<td>Invoice No / Reference</td>
		<td><b>{{invoice.number}}</b> {% if invoice.reference %}[{{invoice.reference}}]{% endif %}</td>
	</tr>
	<tr>
		<td>Description</td>
		<td>{{invoice.description}}</td>
	</tr>
	<tr>
		<td>Untaxed Amount</td>
		<td>{{invoice.untaxed_amount}}</td>
	</tr>
	<tr>
		<td>Tax</td>
		<td>{{invoice.tax_amount}} {{invoice.currency.code}}</td>
	</tr>
	<tr>
		<td>Total Amount</td>
		<td>{{invoice.total_amount}} {{invoice.currency.code}}</td>
	</tr>
	<tr>
		<td>Total Amount To Pay</td>
		<td>{{invoice.amount_to_pay}} {{invoice.currency.code}}</td>
	</tr>
	<tr>
		<td>Amount payable today</td>
		<td>
		{% if invoice.amount_to_pay_today %}
		<b>{{invoice.amount_to_pay_today}} {{invoice.currency.code}}</b>
		{%else%}
		{{invoice.amount_to_pay_today}} {{invoice.currency.code}}
		{% endif %}
		
		</td>
	</tr>
	<tr>
		<td>Invoice Status</td>
		<td>{{invoice.state}}</td>
	</tr>
</table>
<br/>
{% if invoice.comment %}
<h4>Comments:</h4>
<br/>
<p>{{invoice.comment}}</p>
{% endif %}
<a href="/accounts/invoices/{{invoice.id}}/download">
Download ODT</a>
<br/>
<i>To know more about Open Documents visit:
<a href="http://en.wikipedia.org/wiki/OpenDocument">Wikipedia-OpenDocument</a>
</i>
```

Now the final code to be written is for the download of invoice.
This is extracted from : http://www.djangosnippets.org/snippets/365/

```
from django.http import HttpResponse

def download_invoice(request, inv_id):
    inv_id = int(inv_id)
    try:
        party_id = request.user.get_profile().tryton_id
    except:
        party_id = False
    if settings.ENABLE_TRYTON and party_id:
        import base64
        try:
            import cStringIO as StringIO
        except ImportError:
            import StringIO
        from tryton import POOL, DB, USER
        from trytond.tools import Cache
        invoice_obj = POOL.get('account.invoice', type='report')
        cursor = DB.cursor()
        Cache.clean(POOL.database_name)
        try:
            format, report, _, file_name = invoice_obj.execute(cursor,
                    USER, [inv_id], {'id': inv_id, 'ids': [inv_id]})
        finally:
            cursor.close()
            Cache.resets(POOL.database_name)
        reportIO = StringIO.StringIO()
        reportIO.write(base64.decodestring(report))
        wrapper = FileWrapper(reportIO)
        content_type = {
            'odt': 'application/vnd.oasis.opendocument.text',
            'pdf': 'application/pdf',
            }.get(format, 'application/octet-stream')
        response = HttpResponse(wrapper, content_type=content_type)
        response['Content-Disposition'] = 'attachment; filename=%s.%s' % \
                (file_name, format)
        response['Content-Length'] = reportIO.tell()
        reportIO.close()
        return response
    return view_invoice_detail(request, inv_id)
```

That is a very simple integration of Django. This could include a simple payment gateway integration, where a similar return view is called by the gateway passing all the parameters of the transaction and django could call the `pay_invoice` method to pay the invoice.

For a simple example using Pay Pal visit:Django Snippets http://www.djangosnippets.org/snippets/1181/