

# Introduction #

The customs duty is an indirect tax on the import or export of goods in international trade.

The rate of the customs duty is generally defined with reference to the
Harmonized System of Nomenclature. It can be based on the transaction value or on the quantity.

Some countries like Switzerland have different rate (different HS code) for the same product based on a period ([see AFD](http://www.ezv.admin.ch/zollinfo_firmen/04016/04197/index.html?lang=fr)).

The main purpose of the blueprint is to be able to generate customs declarations by storing on incoming and outgoing international moves the customs duty and HS code.

This will allow to generate a report over a set of shipments with the moves grouped by HS code, quantity and duty.

# Implementation #

## customs.tariff\_code ##

  * Code (HS code max 10 digits)
  * Description: `Char` (translatable)

`MatchMixin`:

  * Year Period
  * Country
  * Country Group

## customs.duty\_rate ##

  * Type: `Selection`: Import, Export
  * Country: `Many2One` to country.country
  * Country Group: `Many2One` to country.group
  * Tariff Code: `Many2One` to customs.tariff\_code
  * Base UoM: `Float`
  * UoM: `Many2One` to product.uom
  * Rate Type: `Selection` Amount, Quantity
  * Amount: `Numeric`
  * Currency: `Many2One` currency.currency
  * Start/End Date

## stock.move ##

  * Customs Duty: `Numeric`
  * Customs Duty Currency: `Many2One` currency.currency
  * Tariff Code: `Many2One` customs.tariff\_code

When the international move is created (or modified), it stores the first valid tariff code and compute the customs duty base on the move date, tariff code, quantity, unit price and country. Those fields should stay editable to correct the computed value.

## product.template ##

  * Tariff codes: `Many2Many` product.tariff\_code

# Future Improvements and Ideas #

  * Add support for customs warehouse
  * Import all the HN codes
  * Allow to include customs in the unit price for cost price computation base on [Incoterms](Incoterms.md)

# Links #

  * http://en.wikipedia.org/wiki/Tariff
  * http://en.wikipedia.org/wiki/Combined_Nomenclature
  * https://help.sap.com/saphelp_gts10/helpdata/en/47/28020f97574678e10000000a155369/content.htm?frameset=/en/4c/c6e366e8945dc6e10000000a42189c/frameset.htm&current_toc=/en/b1/8dc5c62c885046ab71fdcddc6ad2c2/plain.htm&node_id=153&show_children=false
  * https://bugs.tryton.org/issue4796
  * https://codereview.tryton.org/12171002