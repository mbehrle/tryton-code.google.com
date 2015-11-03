# Overview #

  * Version number: 1.8.0

# Goals #

## Framework ##

  * ~~Add generic [trigger action](TriggerIntegration.md) on `ModelStorage`~~
  * Replace request with real email with MUA (IMAP), MDA ([Email Integration](EmailIntegration.md))
  * Move images used for the menu (or any tree) on the server side to allow better customization
  * Use BrowseRecord in wizards instead of values
  * Change action in workflow to used named function instead of evaluated python code
  * Add button definition on Models instead on View
  * Improve default value (readonly) in form of relational record from fields with domain
  * Allow to open relational form in new tab
  * Add Drag and Drop in tree view
  * Allow to configure tablespace for Model in trytond.conf
  * Merge tree and list view
  * Add database backend for Oracle
  * Add database backend for Ingres
  * Gantt chart in the client

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

### stock ###

  * Add an indexed period on move with automatic creation and default duration defined on company