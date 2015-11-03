**Implemented**: [stock\_lot](http://hg.tryton.org/modules/stock_lot)

# Introduction #

This document summarizes the functionality to be added and changes to be done to add lots to Tryton stock management.

Module `stock_lot` should only include a basic model with a single Number field. Other modules may want to inherit it to add supplier references, expiry dates, even cost prices.

Lots are not quantity-limited by default although other modules may want to limit them to a single unit per lot for using them as serial numbers, for example.

# Details #

## Lot ##

  * Add 'stock.lot' model with just the "Number" field as fields.Char() and the 'Product' field as a many2one to product.product

## Moves ##

  * Add 'lot' field to stock.move.
  * Adapt assign\_try() and pick\_product() to take 'lot' field into account.

## Products ##

  * Add a new products\_by\_location\_and\_lot() function, similar to products\_by\_location() that will use (product, location, lot) as key and will return the quantities.
  * Add checkboxes to indicate if lots are required in incomming moves, outgoing and/or internal ones.

## Inventories ##

  * Adapt stock.inventory.line. Probably we should split create\_move() in two functions in order to be able to add the values without a need of doing two writes().

  * Replace/remove "inventory\_product\_uniq" constraint to make it unique per inventory + product + lot.

## Shipments ##

  * Add 'lot' field to all shipment views.