

# Introduction #

Intrastat is the system for collecting information and producing statistics on the trade in goods between countries of the European Union (EU). There is also a system for the trade of services.

## Goods ##

The declaration is made of lines with at minima those informations:

  * Code of the destination / origin (according to the way the movement occurs) state
  * Code of the transaction
  * Code of the region of destination / origin
  * Code of the product (according to a EU defined nomenclature)
  * Net mass
  * Additional unit information
  * Value in €
  * Transportation mode
  * Delivery policy

### State codes ###

It's the two letter code of the country of destination / origin.

### Transaction codes ###

They are defined by the country that receive the declaration.
For Belgium they are 9 of them; for France at least 42 …

### Regional code ###

This field is used at least in Beligum and France. For Belgium it is the region of last/first value added to the goods. For France it is the department number where the first expedition / reception occured.

### Product codes ###

Those are defined by the EU: http://eur-lex.europa.eu/legal-content/FR/TXT/HTML/?uri=CELEX:32014R1101&from=FR

Indeed it is the [Combined Nomenclature](http://en.wikipedia.org/wiki/Combined_Nomenclature) which also have a usage for [Tariff](http://en.wikipedia.org/wiki/Tariff)

### Net mass ###

An integer (rounded up) in kg without the packing

### Additional unit information ###

Some products require that additional unit information must be provided (in l, m³, m², …) in this case the net mass is not mandatory.

### Value in € ###

The value is :
  * the value on the invoice (without the service if it is included in the price)
  * without taxes
  * trunked to the integer

NB: France have two rules according to an additional code

### Transportation mode ###

At least something that is somehow common:

  * 1: By ship (on the sea)
  * 2: By railroad
  * 3: By road
  * 4: By plane
  * 5: By postal service
  * 7: By static means (pipeline, …)
  * 8: By ship (on the rivers)
  * 9: By itself (for cars, busses, …)

It is the first mode used when exporting and the last one when importing.

### Delivery policy ###

Those are the incoterms https://en.wikipedia.org/wiki/Incoterms

# Implementation #

I think we should create an intrastat module that will add the products the necessary information (`product code` and eventually `additional unit information`).

A module for the incoterms is also needed. The impact of the incoterms on the other modules must be assessed.

Given the difference from one country to another each country should the use the intrastat module and define itself the process to compute the lines of the intrastat declaration.

It will require the tariff code of CustomsManagement

# Links #
  * National Bank of Belgium Guide: http://www.nbb.be/doc/DQ/f_pdf_ex/basis2015FR.pdf
  * French Custom Guide: http://www.douane.gouv.fr/articles/a10896-comment-remplir-sa-declaration-d-echanges-de-biens