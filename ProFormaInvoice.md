#summary Blueprint Pro Forma Invoice
#labels Phase-Design,Deprecated

# Introduction #
This document shall collect data for the general purpose of a Pro Forma Invoice to precise its use in Tryton.

# Use of Pro Forma Invoice #

Wikipedia:

http://en.wikipedia.org/wiki/Pro_forma :

"In trade transactions, a pro forma invoice is a document that states a commitment from the seller to sell goods to the buyer at specified prices and terms. It is used to declare the value of the trade. It is not a true invoice, because it is not used to record accounts receivable for the seller and accounts payable for the buyer. Simply, a 'Proforma Invoice' is Confirmed Purchase Order where buyer and Supplier agrees on the Product Detail and its cost (usually-Supplier currency) to be shipped to buyer. Sales quotes are prepared in the form of a pro forma invoice which is different from a commercial invoice. It is used to create a sale and is sent in advance of the commercial invoice. The content of a pro forma invoice is almost identical to a commercial invoice and is usually considered a binding agreement although the price might change in advance of the final sale."

http://en.wikipedia.org/wiki/Invoice:

"Pro forma invoice - In foreign trade, a pro forma invoice is a document that states a commitment from the seller to provide specified goods to the buyer at specific prices. It is often used to declare value for customs. It is not a true invoice, because the seller does not record a pro forma invoice as an accounts receivable and the buyer does not record a pro forma invoice as an accounts payable. A pro forma invoice is not issued by the seller until the seller and buyer have agreed to the terms of the order. In few cases, pro forma invoice is issued for obtaining advance payments from buyer, either for start of production or for security of the goods produced."

The latter case of using a pro forma invoice as a document for payment in advance is used at least by some companies in Germany. In many cases a pro-forma invoice is required for customs clearance in import/export business.

# Accounting #

As stated by above sources there usually is no record on accounts receivable or payable.

According to http://de.wikipedia.org/wiki/Proformarechnung there is an additional use in accounting:

If an invoice is not yet existent for the period it belongs to, a pro forma invoice is created to make the moves before closing the year. The pro forma invoice is replaced later by the original.

## Payment in advance ##

A simplified example of those moves for Germany (using intermediate account 'Received prepayment'):
```
Bank
to Account received prepayment
to VAT

Account receivable
to Account revenue
to VAT

Account received prepayment
to VAT
to Account receivable
```
# Discussion #

To provide the payment term "Prepayment" and the correct moves it seems not sufficient to create draft moves in a pro forma invoice (to be able to show payment terms on a pro forma invoice), but to create an additional payment term to do the intermediate moves.

# Links #
http://en.wikipedia.org/wiki/Pro_forma

http://en.wikipedia.org/wiki/Invoice

## german ##
http://www.wirtschaftslexikon24.net/d/pro-forma-rechnung/pro-forma-rechnung.htm

http://de.wikipedia.org/wiki/Proformarechnung

http://de.nntp2http.com/soc/recht/steuern+buchfuehrung/2002/11/db8f82b381e90d8458414c7d4a35d748.html

http://de.nntp2http.com/soc/recht/steuern+buchfuehrung/2002/11/07e2f9127fa3826cf92f909343694b1d.html

http://www.rechnungswesenforum.de/vorkasse-buchungssatz-1491.html