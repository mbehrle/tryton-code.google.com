#adapt sale to b2c environment

# Introduction #

The current sales process in tryton is only adapted to b2b business. B2c handling necessitates some modifications to that logic: the price in a b2c environment must be communicated «all taxes included» to clients.

This document proposes to sum up the requirements, and discuss their possible solutions.

USE CASES: Note that while this is a probable requirement before a pos solution can be implemented, it is tackling a different problem than a pos workflow or interface. Any b2c facing facility (web sites, phone orders, deliveries, pos,...) is impacted.

sources: this includes observations on irc from bechamel, cedk, grasbauer, jcm, sharoonthomas,...<br>
<a href='http://www.tryton.org/~irclog/2012-01-26.log.html'>http://www.tryton.org/~irclog/2012-01-26.log.html</a><br>
<a href='http://www.tryton.org/~irclog/2012-01-30.log.html'>http://www.tryton.org/~irclog/2012-01-30.log.html</a><br>
<a href='http://www.tryton.org/~irclog/2012-01-31.log.html'>http://www.tryton.org/~irclog/2012-01-31.log.html</a><br>
<a href='http://www.tryton.org/~irclog/2012-02-01.log.html'>http://www.tryton.org/~irclog/2012-02-01.log.html</a><br>
<a href='http://www.tryton.org/~irclog/2012-07-03.log.html'>http://www.tryton.org/~irclog/2012-07-03.log.html</a>

<h1>Totals computations</h1>

<h2>Issue</h2>
The current sales process in tryton does all calculations on net price (without tax), and then computes the added taxes.<br>
<br>
This poses problems for b2c because of the rounding.<br>
<br>
Let's take the Belgian vat (which is 21%) as an example, with a product advertised at 1€ (vat included) to b2c clients (say on a web site).<br>
<br>
current behaviour (b2b logic) in tryton for an order of 10 products:<br>
<br>
1€ vat included is a 0,83€ net price.<br>
10x 0,83 = 8,3 total, which makes 10,04 € vat included.<br>
<br>
b2c clients (and the law for b2c environments) expect 10x1€ to be 10€.<br>
<br>
<h2>Proposed solution</h2>
In b2c, all amount computation and rounding must be done on the «tax-included» price. This does not change the price, only rounding is impacted since it is now done on tax included price.<br>
<br>
Of course the usual rules still apply to documents, invoicing,... so net prices and amounts still have to be computed from those tax-included amounts to appear at their usual locations on invoices and all.<br>
<br>
Business clients in EU Intracom and all clients out of EU should still be invoiced without vat.<br>
<br>
<h2>In tryton</h2>
A new sale logic has to be implemented for b2c. It can be added to sale, or a new object can be created for that sole purpose. Both methods have gotchas (see below). Note that the invoice also has to be adapted (in tryton, most computations are actually done in account_invoice, not sale). Both solutions can happen in a separate module, or be included in the base behaviour of tryton.<br>
<br>
A b2c sale must use the tax included price for prices and amounts in lines. That price can be calculated the usual way, or can be stored in the product (see below)<br>
<br>
The sum of all lines becomes the total of the sale (total_amount).<br>
<br>
untaxed_amount has to be computed from total_amount and tax_amount.<br>
<br>
The bunch of the calculations actually happens in account_invoice, where taxes are really calculated. So account_invoice has to be extended to support the b2c logic. (or a new account_invoice_b2c object has to be created for that purpose)<br>
<br>
<h2>Gotchas</h2>
There has been a long multi discusion on irc about the way to implement that: inside sale, or as a new object.<br>
<br>
Implementing it in sale could get messy and complicated. Messy and complicated means bugs. cedk has worked a long time on that problem in another project, and was never satisfied with the solution.<br>
<br>
Implementing it as another object means that all extentions made to sale are not automatically availlable in that new object.<br>
<br>
It is also less flexible because the user has the responsibility to manually decide of the context before creating the document, and it's not possible to switch once started. In this case there is no way to make tryton decide of a default behaviour depending on  the client or any other condition.<br>
<br>
<h2>Exploring the «all integrated» approach</h2>
Here, account_invoice and sale are modified to accomodate b2b and b2c behaviour (internally or by a separate module, this is not the point).<br>
<br>
For each document (invoice, sale,...), the type of behaviour to apply has to be somehow determined. It can be a flag on the document, or a general flag in the configuration, or depend on the client, some product,... the possibilities are endless. To keep all the flexibility while actually implementing a simple mechanism, we can provide a function (let's call it b2borb2c in this document) which returns the behaviour based on a general flag in the configuration, with the default being the current b2b behaviour. More complex or specific behaviours can be implemented later in modules.<br>
<br>
In account_invoice, each calculating method (get_untaxed_amount, get_tax_amount, get_total_amount,...) is modified to accomodate b2c behaviour. Depending on the result of b2borb2c, it applies the correct code path.<br>
<br>
It seems like modifications in the sale object are minimal since it takes all calculations from account_invoice, but this needs further exploration. Anyway if account_invoice can be adapted, sale should not be a big challenge.<br>
<br>
<h2>Exploring the «separate objects» approach</h2>
Here, new objecs (let's call them account_invoice_b2c and sale_b2c for the moment) are created to accomodate b2c behaviour. This seems to only slightly reduce the complexity since all the logic still have to be implemented. But both code paths are completely separated, which can make code reading easier.<br>
<br>
On the other hand, it greatly reduces the flexibility since choosing the correct behaviour is always an operator decision, it cannot be made automatic or depend on configuration.<br>
<br>
<h1>Price calculations</h1>

<h2>Issue</h2>
Currently tryton only stores and calculates sale prices without tax. This poses a display and calculation problem.<br>
<br>
Display problem: the b2c sale price (all taxes included) for a product is not apparent in the product screen. Getting that price for a non business client is not possible without simulating a b2c sale.<br>
<br>
Calculation problem: using the price lists, it seems impossible to base rounding on the tax included price (correct me if I'm wrong, I have not experimented very long with price lists). So getting round prices, or prices like 99,95 , is not possible.<br>
<br>
<h2>Proposed solution</h2>
All these solutions have to be linked to one specific most common tax scenario, because tax included prices vary from country to country. For example a Belgian shop would have his tax included prices linked to the Belgian taxes only.<br>
<br>
There are multiple solutions to the display problem.<br>
<br>
A tax-included price can be stored for products. In a separate "b2c_price" field, or in the usual list_price. If separate, those fields have to somehow be linked by a tax calculation (updating b2c_price should update list_price accordingly). If list_price is used, the sale object must be adapted to know that that price is tax included.<br>
<br>
Or a tax-included price can simply be calculated and displayed on the product form each time the form is displayed.<br>
<br>
The calculation problem also has multiple solutions, but still needs to be explored. Nonetheless, this doesn't preclude working on the other issues, which are broader in scope. (no end-user facing facility can currently use tryton without heavy modifications/approximations)