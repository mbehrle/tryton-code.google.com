

# Introduction #

Tryton should be able to manage customer and supplier deposit.
A deposit is an amount paid by the customer prior to the company providing it
with services or goods.

# Objectives and Features #

A new kind of account "deposit" should be added to be used to compute the
amount deposited by a party.
It should be possible to invoice a product (service) with this kind of account.
On an invoice, it should be possible to recall part of existing deposit in a
line with a negative amount. When posting the invoice, it should never make the
deposit amount of the party below zero.
On sale, it should be possible to define a deposit plan which will create
invoices with deposit. Next invoice will have deposit a negative line from
the previous deposit invoices.

# Implementation #

## Deposit ##

### `account.account` ###

New kind `deposit`

### `party.party` ###

  * deposit: `Function` of `Numeric` with the sum of deposit lines not reconciled

### `account.invoice` ###

Add a wizard to create a negative line using the amount of the party and the
selected `deposit` accounts.
A check on posting will test that the sum of each `deposit` account used is not
negative for the party.

## Sale Deposit ##

### `party.party` ###

  * customer\_deposit\_account: Many2One to `account.account` of kind `deposit`.

### `sale.sale` ###

  * deposit\_amount: Numeric

When deposit\_amount is filled on processing a deposit invoice is created using the party customer deposit account.
No shipment nor invoice will be created until the deposit invoice is paid.
When an invoice is created, the deposit amount is recalled if it was not yet fully done. The amount of deposit is computed by looking at all invoice lines linked to the sale which has the same deposit account as the one created first.

# Future Improvements and Ideas #

<a href='Hidden comment: 
TODO
'></a>

# Links #

  * [Discussion accounting](https://groups.google.com/d/msg/tryton/WRNBmx_Vr44/EzJoOOKto4EJ)
  * [review for account\_deposit](http://codereview.tryton.org/14801002)