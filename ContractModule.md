# Service Contract Module #

Modules to manage service contracts. (not projects or timesheets)

Designed in two modules:

  * **contract**: Management services and contracts (model and views)
  * **contract\_invoice**: Generate account.invoice.line from contracts (cron)

We separate in two modules because is not necessary use contract\_invoice to manage contracts

# Contract #

## Service (contract.service) ##

  * Name. Name of service
  * Product. Product related at service
  * Qty. Qyt products (numeric)
  * Interval (day, week, month, year)
  * Interval Count
  * Note

## Contract (contract.contract) ##

  * Reference (sequence)
  * Party
  * Service (contract.service)
  * State: draft, active, hold, canceled
  * Start date
  * Finish date
  * Note

## Groups ##

  * **Contract Manager**. Access to services & co.
  * **Contract**. Access to Contract

# Contract Invoice #

Generate account.invoice.lines from contracts

## Service (contract.service) ##

  * Method: selection [('default','python')]
  * Qty Formula. Python expresion to evaluate (calculate qty + description from another rows (optional). Return a dict {'qty','description'}. Invisible when method is default.
  * Request group. Group user to send a request (notification)
  * Analytic Account (default)

## Contract (contract.contract) ##

  * Account invoice lines (o2m)
  * Analytic Account (custom)

## Create Account Invoice Lines ##

### Option A. Multy crons ###

In contract a new field m2o, `cron` (create ir.cron when active contract). This cron has information when create next account.invoice.line.

Cons: create a lot of crons.

### Option B. One cron ###

In contract a new field date, `next execution`.

In ir.cron only we have a cron. This cron run every x minutes and review all contracts between last execution to now. If exists a contract and next executation field is between this date, create a new account.invoice.line.

Cons: Not generate account.invoice.line in exactly time.