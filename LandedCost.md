

# Introduction #

There could be many different kind of cost that will affected the cost price of products. The module `purchase_shipment_cost` can not manage all the cases as it is based only on shipment cost and with the prerequisite to know the cost at the reception.

Tryton must have a way to record landed cost after the reception of the shipments. The idea is to create a new document that will link supplier invoice lines for cost with shipments. The document will add to each moves the new costs.

There are special cases with `account_stock_continental` where if the unit price of a move done is changed, a correction accounting move will be required and idem for `account_stock_anglosaxon` but only for the input anglo-saxon quantity (already invoiced) and for the ratio of quantity already sold since divided by the quantity at the date of reception.

Tryton will also need to be able to recompute the average and the FIFO cost price from at least the beginning.

Once the landed cost applied, the invoice lines should be linked to the stock moves updated.

# Implementation #

## `account.landed_cost` ##

  * Shipments: `Many2Many` to `stock.shipment.in`
  * Invoice Lines: `Òne2Many` to `account.invoice.line` for only landed cost products
  * Allocation Method: `Selection`: by value
  * State: `Selection`: draft, applied

## `product.template` ##

  * Landed cost: Boolean only for service

# Future Improvements #

  * Manage automatically the update of cost price with `account_stock*` modules
  * Allow to deduce of the cost allocation previous shipment cost

# Links #

  * https://bugs.tryton.org/issue4726