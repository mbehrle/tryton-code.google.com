#summary Howto create a chart of accounts (draft)
#labels Phase-Implementation

# Introduction #

You want to use Tryton, but it doesn't support the accounting system in your country. This document will help you to add such support.

This document is in **draft** status, so don't take anything explained here as true, until the draft status is removed.

# Data structures #

## account.account.type.template ##

  * name (required)
  * sequence (required): Use to order the account type.
  * parent
  * balance\_sheet
  * income\_statement
  * display\_balance (required, default: debit-credit)

## account.account.template ##

  * name (required)
  * code
  * type (required, except for view kind)
  * parent
  * reconcile: Whether the account can be used for reconciliation.
  * kind (required)
  * deferral (not useful for kind == view)

## account.tax.group ##

  * name (required)
  * code (required)

## account.tax.code.template ##

  * name (required)
  * code
  * parent
  * account (required)

## account.tax.template ##

  * name (required)
  * description (required): The name that will be used in reports.
  * group (required)
  * sequence: Use to order the taxes
  * amount: In company's currency
  * percentage: In %
  * type (required)
  * parent
  * invoice\_account:
  * credit\_note\_account
  * invoice\_base\_code
  * invoice\_base\_sign: 1 or -1
  * invoice\_tax\_code
  * invoice\_tax\_sign: 1 or -1
  * credit\_note\_base\_code
  * credit\_note\_base\_sign: 1 or -1
  * credit\_note\_tax\_code
  * credit\_note\_tax\_sign: 1 or -1
  * account (required)

## account.tax.rule.template ##

  * name (required)
  * account (required)

## account.tax.rule.line.template ##

  * rule (required)
  * group (required)
  * tax
  * sequence

# Notes #

This is a place holder where I'm storing brief explanations of Tryton elements to be used in longer explanations as we develop this document.

  * kind payable: An account that could be used to do payments.
  * kind receivable: An account that could be used to get payments.
  * first level (root) account.account.type.template need to look like:
```
        <record model="account.account.type.template"
            id="[[HERE_YOUR_ID]]">
            <field name="name">[[HERE YOUR ACCOUNT CHART TYPE NAME]]</field>
            <field name="sequence" eval="10"/>
        </record>
```
  * Do not use balance\_sheet on root account.account.type.template, it produce the error:
> > "The field Type on account is required."