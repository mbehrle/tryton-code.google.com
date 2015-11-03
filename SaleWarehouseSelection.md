# Introduction #

This document will explain the proposed sale\_warehouse\_selection module.

# Rational #

It is to allow to change the default warehouse per sale line.
To achieve this, the new concept of "warehouse selection rule" will be added similar to the price lists or the tax rule. This rules will be applied in the Function field `warehouse` of the `sale.line` and as it is already [supported](http://hg.tryton.org/modules/sale/file/84876ff7ef2d/sale.py#l763) the sale will group shipment based on the line warehouse.

# Details #

## Sale Line ##

  * Extend `get_warehouse` to apply `sale.warehouse_selection.rule`

## Warehouse Selection Rule ##

  * New Model named `sale.warehouse_selection.rule`
  * Fields:
    * `company`
    * `sequence` (for order)
    * `origin_warehouse`
    * `product`
    * `warehouse` (new warehouse)
  * A class method `apply(sale_line)` which will return the warehouse
  * An instance method  `match(sale_line)` which will return True if rule match the criteria