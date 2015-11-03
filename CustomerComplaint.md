

# Introduction #

Tryton should be able to manage customer complaint.
When a complaint is registered, the company should take actions to resolve the complaint. Those action should be validated by a third person.

# Objectives and Features #

  * Register complaint
  * Qualify the complaint
  * Define actions to take
  * Process the actions

# Implementation #

## `sale.complaint` ##

  * reference: `Char`
  * date: `Date`
  * customer: `Many2One` to `party.party`
  * address: `Many2One` to `party.address`
  * company: `Many2One` to `company.company`
  * description: `Text`
  * employee: `Many2One` to `company.employee`
  * origin: `Reference`
  * type: `Many2One` to `sale.complaint.type` with domain on origin
  * state: `Selection`: 'draft', 'waiting', 'approved', 'rejected', 'done', 'cancelled'
  * actions: `One2Many` to `sale.complaint.action`

The complaint could be reset to draft once done or cancelled. And if actions were already proceed, they will stay as-is in read-only. This will allow to add new actions to the complaint.

## `sale.complaint.type` ##

  * name: `Char`
  * origin: `Many2One` to `ir.model.model`

## `sale.complaint.action` ##

  * complaint: `Many2One` to `sale.complaint`
  * action: `Selection`:
    * Create a sale return for the sale origin
    * Create a sale return for the sale line origin for an optional quantity and an option unit price
    * Create a credit note for the invoice origin
    * Create a credit note for the invoice line origin for an optional quantity and an optional unit price
  * quantity: `Float`
  * unit price: `Numeric`
  * sale lines, invoice lines: `Many2Many` to filter document creation.

The list of action should be extendible per modules.
The action will be performed when the complaint is done.

## `sale.sale` ##

  * Add a relate to linked complaints.

# Future Improvements and Ideas #

  * Historize the complaint
  * Add predefined actions on type
  * Some report complaint rate over time per type etc.

# Links #

  * [Discussion](https://groups.google.com/forum/#!msg/tryton/S6vSrcRUEsQ/YTmowkfF9uoJ)
  * [Codereview](http://codereview.tryton.org/7991003)