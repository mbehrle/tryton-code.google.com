

# Introduction #

Tryton should allow to enter budget for accounts or analytic accounts.
A budget is a plan over a period to define the balance per sets of accounts.

# Objectives and Features #

It should be possible to define a budget based on accounts or analytic accounts.
It should be possible to compare actual with budget.

# Implementation #

`account_budget` should define Mixin to be reused for other similar modules.

## Budget ##

### `account.budget` ###

  * name: `Char`
  * company: `Many2One` to `company.company`
  * fiscalyear: `Many2One` to `account.fiscalyear`
  * parent: `Many2One` to `account.budget`
  * children: `One2Many` to `account.budget`
  * amount: `Numeric` in company currency
  * accounts: `Many2Many` of `account.account`
  * balance: `Function` of `Numeric` with the sum of accounts balance over the fiscal year including the children budget.
  * periods: `One2Many` to `account.budget.period`

sum of period must be <= than amount

sum of children must be <= than amount

account must be only once per budget root

### `account.budget.period` ###

  * budget: `Many2One` to `account.budget`
  * period: `Many2One` to `account.period`
  * amount: `Numeric` in company currency
  * balance: `Function` of `Numeric` with the sum of accounts balance over the period.

unique per budget and period

A wizard should allow to copy the entire budget tree but changing the fiscal year by a new one (skipping the period as no direct link could be done). It must also have an option to zero the amount.

A wizard should allow to distribute the amount of a budget over all the period using a selected method (default: evenly).

## Analytic Budget ##

### `analytic_account.budget` ###

Same as `account.budget` but over date period.


# Future Improvements and Ideas #

  * Modules base on sale, project etc.
  * Budget debit/credit amount