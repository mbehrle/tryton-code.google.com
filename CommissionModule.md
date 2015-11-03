

# Introduction #

Tryton should be able to manage the commission to send to agent of a sale.


# Objectives and Features #

  * commission computation base on plan
  * commission on invoice posted or paid

# Implementation #

## Commission ##

### `commission.agent` ###

  * party: `Many2One` to `party.party`
  * type: `Selection`: Agent Of, Principal Of
  * company: `Many2One` to `company.company`
  * plan: `Many2One` to `commission.plan`
  * currency: `Many2One` to `currency.currency`
  * pending\_amount: `Function` of `Numeric` with the sum of amount of lines not invoiced

### `commission.plan` ###

like price\_list

  * name
  * product: `Many2One` to `product.product` with type `service`
  * method: `Selection`: On Posting, On Payment
  * lines

### `commission` ###

  * origin: `Reference`
  * date: `Date`
  * agent: `Many2One` to `commission.agent`
  * product: `Many2One` to `product.product` (from `commission.plan`)
  * amount: `Decimal` in the agent's currency
  * invoice\_line: `Many2One` to `account.invoice.line` with the type depending on type of agent
  * invoice\_state: `Function` returning the state of the linked invoice
  * type: `Selection`: `in`, `out` from type of agent

### `account.invoice` ###

  * agent: `Many2One` to `commission.agent`

### `account.invoice.line` ###

  * principal: `Many2One` to `commission.agent`
  * commissions: `One2Many` to `commission.line` using `origin`
  * from\_commissions: `One2Many` to `commission.line` using `invoice_line`

### `sale.sale` ###

  * agent: `Many2One` to `commission.agent`

### `sale.line` ###

  * principal: `Many2One` to `commission.agent`


### `product.template` ###

  * principals: `One2Many` to `commission.agent`

A commission line will be created on posting of the invoice for each line with
the agent as party. The lines will be removed or a negative line will be
created if the invoice is cancelled.

The date of the commission line will be set accordingly to the method.

The amount of the line will be computed using the plan for each invoice line.

A wizard will allow to generate invoices from commission line over a period.
The invoice line will be grouped by product and agent.

# Future Improvements and Ideas #

  * Allow the agent to reduce his commission to reduce the price.
  * Historize the commission plan
  * Add reporting on agent
  * Support pre-paid commission
  * Add support for `project_invoice`
  * Add support when agent is the customer. The base amount of taxes must be deduced by the commission and the commission will be without taxes.

# Links #

  * [Discussion general](https://groups.google.com/forum/#!topic/tryton/ycKk-bTRx_4)
  * [Discussion implementation](https://groups.google.com/d/topic/tryton-dev/WYaskDNtkLw/discussion)
  * [review for commission](http://codereview.tryton.org/13641002)
  * [review for commission waiting](http://codereview.tryton.org/6621002)