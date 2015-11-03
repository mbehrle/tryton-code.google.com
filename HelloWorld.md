

# Module Creation #

We will start by creating a module called `HelloWorld`, in the beginning our module will only have an entry in the main menu.  We will add more features later on. Now let's get started.

## Step 1 for Tryton : Creating the `HelloWorld` module ##

### Create a directory for your module ###

Create a directory called **helloworld** in the _trytond/modules_ directory.

In Linux you create the directory like this:

```
cd  /usr/local/tryton/trytond/trytond/modules/
mkdir helloworld
```

### Init file ###

Inside this directory put the file **`__init__.py`**, this file will call our _.py_ files, as in the following line/lines:

**for tryton < 2.6:**

```
from hello import *
```


**for tryton 2.8:**

```
from trytond.pool import Pool
from .hello import *


def register():
    Pool.register(
        Hello,
        module='helloworld', type_='model')
```


### Config File ###

**for tryton < 2.6:**

Create the file _`__tryton__.py`_ with the following lines:

```
{
    'name' : 'Hello World',
    'version' : '0.0.1',
    'author' : 'nickname',
    'email': 'correo@example.com',
    'website': 'http://www.tryton.org/',
    'description': 'Hello World with menus',
    'depends' : [
        'ir',
    ],
    'xml' : [
        'hello.xml',
    ],
    'translation': [
    ],
}
```

**for tryton 2.8:**


Create the file _'tryton.cfg'_ with the following lines:

```
[tryton]
version=2.8.0
depends:
  ir

xml:
  hello.xml
```

**Note**: The version number is optional, meaning: the module would work without it

**Note2**: Every external module for tryton must have at least ir in dependencies


### hello.py ###


Now we're going to create a file called hello.py with the following lines

**for tryton < 2.6**

```
from trytond.model import ModelView, ModelSQL, fields
class Hello(ModelSQL, ModelView):
    'HelloWorld'
    _name = 'hello.hello'
    _description = __doc__

Hello()
```


**for tryton 2.8:**

```
from trytond.model import ModelView, ModelSQL, fields

__all__ = ['Hello']


class Hello(ModelSQL, ModelView):
    "HelloWorld"
    __name__ = "hello.hello"
```

### hello.xml ###

In the last file _hello.xml_ we put:

```
<?xml version="1.0"?>

<tryton>
    <data>
        <menuitem name="Hello World" id="menu_hello_world" sequence="10" icon="tryton-list"/>
    </data>
</tryton>
```

With this we have the first module to import, which will show in the main menu without any information.


**Note** If you have problem with the icon, remove it from the _hello.xml_ file.

**Note2** If you have problems activating/installing your new module, try restarting the tryton server ($ services tryton-server restart)

## Step 2: Extending our model and adding views ##

Now that our module is working we will add some more features. Let's extend our model and add two views to the module.  To extend our model we edit the file hello.py and add these two fields to the class Hello:

```
    name = fields.Char('Name')
    greeting = fields.Char('Greeting')
```

with this our file will be:

**tryton < 2.6**

```
from trytond.model import ModelView, ModelSQL, fields
class Hello(ModelSQL, ModelView):
    'HelloWorld'
    _name = 'hello.hello'
    _description = __doc__
    name = fields.Char('Name')
    greeting = fields.Char('Greeting')

Hello()
```

**tryton 2.8**

```
from trytond.model import ModelView, ModelSQL, fields

__all__ = ['Hello']


class Hello(ModelSQL, ModelView):
    "Hello World"
    __name__ = "hello.hello"

    name = fields.Char('Name')
    greeting = fields.Char('Greeting')
```

This tells tryton to create two fields, both of type Varchar or String.

After this we edit the file _hello.xml_ and add the following groups of lines.  Each group of lines is preceded with an explaination.  For more information read the Views section of the Tryton documentation found at tryton.org.

First we create a view of type tree which will list our model **hello.hello** with its two fields: **name** and **greeting**.

```
        <!-- View for tree-->
        <record model="ir.ui.view" id="hello_view_tree">
            <field name="model">hello.hello</field>
            <field name="type">tree</field>
            <field name="arch" type="xml">
                <![CDATA[
                <tree string="Hello World">
                    <field name="name"/>
                    <field name="greeting"/>
                </tree>
                ]]>
            </field>
        </record>
```

Secondly we create a view of type form which will show a single record of our model **hello.hello** in a form with with the two labels and two fields: **name** and **greeting**.

```
       <record model="ir.ui.view" id="hello_view_form">
            <field name="model">hello.hello</field>
            <field name="type">form</field>
            <field name="arch" type="xml">
              <![CDATA[
              <form string="Hello">
                <label name="name"/>
                <field name="name"/>
                <label name="greeting"/>
                <field name="greeting"/>
              </form>
              ]]>
            </field>
       </record>
```

Create an event to open a new tab(window). This event will be used to connect the menu **Hello World** with the tree and form views.  Note the id of this event as it will be used later.
```
        <!-- View for the main menu and the event -->
        <record model="ir.action.act_window" id="act_hello_world_form">
            <field name="name">Hello World</field>
            <field name="res_model">hello.hello</field>
        </record>
```

With the ids of the event and the two views defined before we add two fragments to attach the **id** to the **window** and the **view** used to populate the window.  The field **view**  indicates which **view** will be used and the field **act\_window** indicates the **event** that will activate the view.

```
        <!-- View that connect the form in the tree with the specification -->
        <record model="ir.action.act_window.view" id="act_hello_form_view1">
            <field name="sequence" eval="10"/>
            <field name="view" ref="hello_view_tree"/>
            <field name="act_window" ref="act_hello_world_form"/>
        </record>

        <!-- View for the edition or the Form of hello-->
        <record model="ir.action.act_window.view" id="act_hello_form_view2">
            <field name="sequence" eval="20"/>
            <field name="view" ref="hello_view_form"/>
            <field name="act_window" ref="act_hello_world_form"/>
        </record>
```

We use ids for each record throughout the xml file.  This allows other modules to identify and reuse or extend parts of our module.

Now finally at the end of our xml file we add one more fragment to join the views with the last menu:

```
        <menuitem parent="menu_hello_world" sequence="1"
            id="menu_hello_world_form" icon="tryton-list" action="act_hello_world_form"/>
```

## Step 3: Creating a report ##

Add the following lines to the file 'hello.xml' into the /data tag:

```
        <record model="ir.action.report" id="report_hello">
            <field name="name">Hello</field>
            <field name="model">hello.hello</field>
            <field name="report_name">hello.helloworld</field>
            <field name="report">helloworld/hello.odt</field>
        </record>
        <record model="ir.action.keyword" id="report_hello_world">
            <field name="keyword">form_print</field>
            <field name="model">hello.hello,0</field>
            <field name="action" ref="report_hello"/>
        </record>
```

**for tryton 2.8**:
replace 'hello.hello,0' with 'hello.hello,-1'


Now create the file hello.odt inside the directory .../trytond/trytond/modules/helloworld.

In this file add the lines:

```
<for each="hello in objects">
<hello.name>
</for>
```

Each line, must be added using OpenOffice writer, in the menu: Insert->Fields->Others..., in the tag 'Functions', with the type 'Placeholder' and the format 'Text', and fill the field Placeholder with each line, vg: 'for each="hello in objects"'.

Other way to do this is copying the file '.../trytond/trytond/modules/party/label.odt', and editing it by pressing the right button in the mouse, and copying and pasting to add new lines.


### you want to learn more ###

Have a look at http://hg.tryton.org/2.6/training/ there you'll find hg changesets to help you further on in module development..

**Note:** usage is descriped in repository description at http://hg.tryton.org/2.6/ ..
**Note2:** you'll need to have mercurial 'mq' expension activated