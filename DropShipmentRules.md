

**Rejected**: the rule pattern doesn't seem to be a good one.

# Introduction #

In some cases, a company might want to have more control over the drop shipment mechanism than it is currently possible. For example, small quantities of product might be delivered from the company's warehouse but bigger orders should use the drop shipment feature provided by Tryton.

# Objectives and Features #

  * Whether to apply or not drop shipping will be defined by rules
  * Easily extensible with specific modules to take into account different shipment policies

# Implementation #

Module name: 'sale\_supply\_drop\_shipment\_rules'

## Models ##

Those models were designed to mimic the Tax Rule mechanism that is already present.
The first matching rule will define, per 'sale.line', whether or not the drop shipment mechanism is to be applied.

### 'sale.drop\_shipment.rule' ###

  * 'name': char
  * 'company': many2one to 'company.company'
  * 'lines': one2many to 'sale.drop\_shipment.rule.line'

### 'sale.drop\_shipment.rule.line' ###

  * 'rule': many2one to 'sale.drop\_shipment.rule'
  * 'sequence': integer
  * 'apply\_drop\_shipment': selection Yes / No

### 'stock.location' ###

  * 'drop\_shipment\_rule': many2one to 'sale.drop\_shipment.rule'