# Overview #

  * Version number: 2.2.0

# Goals #

## Framework ##

  * ~~Dropping Python 2.5~~
  * Add Async call method
  * ~~Change action in workflow to used named function instead of evaluated python code~~
  * Add button definition on Models instead on View
  * Replace request with real email with any MUA (through IMAP) and MDA (procmail like) ([Email Integration](EmailIntegration.md))
  * ~~Replace search widgets by a single widget~~
  * Use classes in pool and replace instance method by class method
  * Add context management in Proteus
  * Implement methods on relation fields in Proteus (add, remove, new etc.)
  * Replace nested view by reference id

## Modules ##

### account\_invoice ###

  * Add a reference field on the invoice to provide links to other models (e.g. sale, purchase)
  * Store function fields when invoice is in read-only state

### account ###

  * Change code rules on taxes to use a one2many instead of fixed fields
  * Add a sequence on tax code

### production ###

  * Integrate production module

### purchase ###

  * Add historization of quotation
  * Allow to customize purchase.product\_supplier to handle delivery\_time depending of quantity
  * Cancel draft moves and draft invoices when canceling purchase order
  * Store function fields when purchase is in read-only state

### sale ###

  * Add historization of quotation
  * Cancel draft moves and draft invoice when canceling sale order
  * Store function fields when sale is in read-only state