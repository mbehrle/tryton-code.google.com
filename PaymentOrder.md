

# Introduction #

It is common in several countries send payment orders to the bank to pay/receive several payments together. In these cases we need to create a payment order that include several payments lines. These payment lines are unreconciled account move lines not included in other payment orders. They include the amount, currency and maturity date of the payment.

# Objectives and Features #

  * The payment orders allow negative payment amounts. So we can have payment orders for supplier invoices (pay money) and refund supplier invoices (return or receive money). Or for client invoices (receive money) and refund client invoices (return or pay money).
  * Three types of payment orders: Payable payment orders (from supplier invoices), receivable payment orders (from client invoices) and payable-receivable orders (for all kind of invoices). So we can make payment orders to pay the payment of supplier invoices, to receive the payments of client invoices or to mix both of them.
  * Creation of payment orders: The account.move.lines to add could be filtered by party and maturity date.
  * Payment journal: It is a new concept that relates an account journal of a company to process payment orders of a specific type. It helps creating configurations for payment orders. For example, a company could use different account journals to pay different payment order types, then several payment journals could be created.
  * Easily extensible with specific modules to add several file formats to export a payment order (and send it to the company bank, for example, to process those payments).

# Implementation #

Module name: 'account\_payment'

## Models ##

### 'account.payment.journal' ###

  * 'name': char
  * 'company': many2one to 'company.company'
  * 'currency'
  * 'process\_method': selection: 'manual' (to be extended by other modules)

### 'account.payment.group' ###

  * 'reference': fill with sequence

### 'account.payment' ###

  * 'company'
  * 'journal'
  * 'kind': selection: 'payable' or 'receivable'
  * 'party'
  * 'date'
  * 'amount': default to 'payment\_amount' of 'line'
  * 'currency': function from 'account.payment.journal'
  * 'line': many2one to 'account.move.line':
    * on account 'payable' or 'receivable'
    * linked to 'party'
    * not reconciled (in 'draft' state)
    * 'payment\_amount' != 0
    * second\_currency == currency if not company currency
  * 'description'
  * 'group': many2one to 'account.payment.group'
  * 'state': selection: 'draft', 'approved', 'processing', 'succeeded', 'failed' (for workflow)

### 'account.move.line' ###

  * 'payment\_amount': function:
    * only for 'receivable' or 'payable'
    * (debit - credit) - linked payments not 'failed'
    * in second currency or company currency

## Wizards ##

### 'account.payment.pay' ###

  * Run on 'account.move.line' (from view below)
  * Warn about non-reconciled credit (or debit).
  * Ask 'account.payment.journal'
  * Create a default 'account.payment' for the line

### 'account.payment.process' ###

  * Run on 'account.payment' per 'journal' and 'kind'
  * Warn for any duplicate payment (0 > 'payment\_amount')
  * Room to extend the process (like generate file)
  * Set state to 'processing' and 'group'

## Views ##

  * A list of 'account.move.line' for account kind 'payable', not reconcilied
> > (and payment\_amount > 0), posted with fields:
      * 'origin'
      * 'party'
      * 'maturity\_date'
      * 'account'
      * 'debit'
      * 'credit'
      * 'amount\_second\_currency'
      * 'payment\_amount'

  * A 'tree\_open' action on 'account.payment.journal' to open linked payments.

# Future ideas #

  * Show on journal current amount and forecast amount (after payments)
  * Sent email for late payment
  * Allow to specify an amount to dispatch on many lines in "pay" wizard
  * Retrieve extra information about payment from the move line (like bank account)