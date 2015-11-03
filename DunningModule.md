

**Implemented**: [account\_dunning](http://hg.tryton.org/modules/account_dunning)

# Introduction #
Tryton currently lacks the functionality to remind customers of unreconciled and overdue receivables.


# Objectives and Features #
  * multiple dunning procedures
  * multiple levels per dunning procedure
  * default dunning procedure for a party
  * see the current level for every dunning
  * reset the current level for a dunning
  * set an entry-level dunning block


# Implementation of Module `account_dunning` #
## Models ##
### `account.dunning.procedure` ###
  * `name`

### `account.dunning.level` ###
  * `procedure`: `Many2One` to `account.dunning.procedure`
  * `sequence`: `Integer` to order
  * `days`: the number of overdue days
  * `test(move)`: method to test if the level can be reached.

### `account.dunning` ###
  * `company`
  * `line`: `Many2One` to `account.move.line` (UNIQUE)
  * `procedure`: `Many2One` to `account.dunning.procedure`
  * `level`: `Many2One` to `account.dunning.level`
  * `block`: `Boolean` to prevent to raise the level
  * `state`: `Selection`: Draft, Done
  * `active`: `Function`, `Boolean`: `True` if `line` is reconciled

### `party.party` ###
  * `dunning_procedure`: the default dunning procedure, `Property`, `Many2One` to `account.dunning.procedure`

## Wizards ##
### `account.dunning.create` ###
  * loop over Done dunning:
    * search the first next level where `test` is true
    * if new level is found, set to it and reset the state to draft
  * search for new line for dunning (on account `receivable`):
    * `procedure` is the default of party
    * `level` is the first level where `test` is true
    * `state` is Draft

### `account.dunning.proceed` ###
  * Run over dunning
  * Set `state` to Done

# Implementation of Module `account_dunning_letter` #
## Models ##
### `account.dunning.level` ###
  * `print_on_letter`: Boolean

### `account.dunning.proceed` ###
  * add launch of report

## Reports ##
### `account.dunning.letter` ###
  * group dunning by party
  * add non-reconciled payments
  * skip party if sum dunning < sum payments

# Future Improvements and Ideas #
  * charge dunning fees
    * fixed (per receivable/letter)
    * interest (on total/remaining amount)
  * minimum receivable amount
  * selectable grouping
    * by party
    * by dunning level
    * none

# Links #

  * [Code review](http://codereview.tryton.org/939002/)
  * [Old Code review](http://codereview.tryton.org/517002/)

  * Prototype
    * [Source](https://bitbucket.org/kantntreiber/trytond_account_dunning)
    * [Module documentation](https://bitbucket.org/kantntreiber/trytond_account_dunning/src/d952c442a14503e5948e628a87c8dd63ce1bc1f2/doc/index.rst?at=default)