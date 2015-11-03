# Overview #

  * Version number: 2.4.0

# Goals #

## Framework ##

  * ~~Add button definition on Models instead on View~~
  * ~~Replace nested view by reference id~~
  * Support different tables for Property fields
  * Migrate to GTK-3
  * ~~New wizard design~~
  * ~~Session in Database~~
  * WSGI
  * Replace request with real email with any MUA (through IMAP) and MDA (procmail like) ([Email Integration](EmailIntegration.md))
  * Use classes in pool and replace instance method by class method
  * Add context management in Proteus
  * Implement methods on relation fields in Proteus (add, remove, new etc.)

## Modules ##

### account\_invoice ###

  * Add a reference field on the invoice to provide links to other models (e.g. sale, purchase)

### account ###

  * Don't allow mixing account chart of different companies
  * Change code rules on taxes to use a one2many instead of fixed fields
  * Add a sequence on tax code

### production ###

  * Integrate production module

### purchase ###

  * Add historization of quotation
  * Allow to customize purchase.product\_supplier to handle delivery\_time depending of quantity
  * Cancel draft moves and draft invoices when canceling purchase order
  * ~~Store function fields when purchase is in read-only state~~

### sale ###

  * Add historization of quotation
  * Cancel draft moves and draft invoice when canceling sale order
  * ~~Store function fields when sale is in read-only state~~