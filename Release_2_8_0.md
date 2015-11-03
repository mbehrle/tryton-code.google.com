# Overview #

  * Version number: 2.8.0

# Goals #

## Framework ##

  * Support different tables for Property fields
  * WSGI
  * Replace request with real email with any MUA (through IMAP) and MDA (procmail like) ([Email Integration](EmailIntegration.md))
  * Use python-sql
  * Add GIS support
  * ~~Change constraints API for improved error messages~~

## Modules ##

### account ###

  * Don't allow mixing account chart of different companies
  * Change code rules on taxes to use a one2many instead of fixed fields
  * Add a sequence on tax code

### purchase ###

  * Add historization of quotation
  * Allow to customize purchase.product\_supplier to handle delivery\_time depending of quantity

### sale ###

  * Add historization of quotation