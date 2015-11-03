#summary Goals for release 1.6.0

# Overview #

  * Version number: 1.6.0

# Goals #

## Framework ##

  * ~~Add JSON-RPC interface~~
  * ~~Improve [SSL implementation](RequirementsSSL.md)~~
  * Gantt chart in the client
  * Add generic trigger action on ModelStorage
  * Replace request with real email with MUA (IMAP), MDA ([Email Integration](EmailIntegration.md))
  * ~~Add database backend for MySQL ([Why PostgreSQL Instead of MySQL](http://wiki.postgresql.org/wiki/Why_PostgreSQL_Instead_of_MySQL_2009))~~
  * Add database backend for Oracle
  * Add database backend for Ingres
  * Improve default value (readonly) in form of relational record from fields with domain
  * Allow to open relational form in new tab
  * Merge tree and list view
  * Add Drag and Drop in tree view
  * Allow to configure tablespace for Model in trytond.conf
  * Use BrowseRecord in wizards instead of values
  * ~~Use a versioned configuration directory for tryton~~
  * ~~Remove evaluated python expression strings on the client side~~
  * Move images used for the menu (or any tree) on the server side to allow better customization
  * ~~Use standard form for attachments.~~
  * ~~Remove "child1" and "child2" tags for a unique "child"~~
  * ~~Use instance of other fields in Function/Property fields~~

## Modules ##

### account\_invoice ###

  * Add a reference field on the invoice to provide links to other models (e.g. sale, purchase)
  * Store function fields when invoice is in read-only state

### account ###

  * Change code rules on taxes to use a one2many instead of fixed fields
  * Add a sequence on tax code

### currency ###

  * Add wizard to update currencies rate from different websites

### google\_maps ###

  * Add html report for a map with selection of parties

### purchase ###

  * Add historization of quotation
  * Allow to customize purchase.product\_supplier to handle delivery\_time depending of quantity
  * Cancel draft moves and draft invoices when canceling purchase order
  * Store function fields when purchase is in read-only state

### sale ###

  * Add historization of quotation
  * Cancel draft moves and draft invoice when canceling sale order
  * Store function fields when sale is in read-only state

### sale\_opportunity ###

  * Include the module [sale\_opportunity](http://mercurial.intuxication.org/hg/sale_opportunity) as standard module.

### stock ###

  * Add an indexed period on move with automatic creation and default duration defined on company