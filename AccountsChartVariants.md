# Introduction #

This document details the proposal of the new account\_chart\_variant module.

# Rationale #

As exposed on https://groups.google.com/forum/#!searchin/tryton-dev/account_es/tryton-dev/Z03bdDCb5X8/rBLj-yWwnrIJ in Spain we have two charts of accounts with more than 1000 accounts in common. This module tries to  to avoid data duplication, by allowing to create a chart of accounts with diferents accounts.

# Details #

The module will add a new model to specify chart variants.

Also the module will add the variant field in the create/update chart of accounts wizards, in order to let the user select the desired variant

## Models ##

### account.chart.variant ###

This model stores the variants of a chart of accounts.

  * Fields:
    * `name`: Translatable Char
    * `account`: Many2One to account.account with parent set to null (Chart of accounts)

### account.account.type.template ###

  * Fields to add :
    * `variant`: not required Many2One to `account.chart.variant`

  * Function to modify:
    * create\_type`: Will not create type if variant is diferent from the variant selected on the wizard. It will create the type if no variant especified on the template.
    * update\_type`: Will not create type if variant is diferent from the variant selected on the wizard. It will create the type if no variant especified on the template.
### account.account.template ###

  * Fields to add :
    * `variant`: not required Many2One to `account.chart.variant`

  * Function to modify:
    * create\_account`: Will not create account if variant is diferent from the variant selected on the wizard. It will create the account if no variant especified on the template.
    * update\_account`: Will not create account if variant is diferent from the variant selected on the wizard. It will create the account if no variant especified on the template.


NOTE: Currently the variant is not introduced in tax's models (as currently not needed), but it can be introducied if anyone needs.

# Discussion #

https://groups.google.com/forum/#!topic/tryton/r16rr0HNX90

# Implementation #

http://codereview.tryton.org/3981002