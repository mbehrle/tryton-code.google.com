

# Introduction #
This page is for logging collaborated manual test results. Tryton is additional tested by an automated test framework. See http://tests.tryton.org/~test/ and http://tests.tryton.org/~test/sqlite/ for results.

If you like to share your experience, just put your nickname and a result shortcut into the fields you tested. In general it is no problem when there are many people testing the same functionality, just put your results into the table, too. Please try to test parts which are untested.
  * Download and install the latest development version of Tryton
    * http://code.google.com/p/tryton/wiki/InstallationMercurial
  * Test all actions and workflows in expected functionality.
  * Test if reports generate output
  * Test translations for:
    * de: German
    * en: English
    * es: Spanish
    * fr: French
    * _add your language here_

If you find bugs, create for each bug an issue in [roundup](http://bugs.tryton.org/). Please collect the issue number in the column 'Issues'.

## Nicknames ##

| Nick | Name | Comments |
|:-----|:-----|:---------|
| us   | Udo Spallek |Details in my [testing plan](http://spreadsheets.google.com/ccc?key=tU28D4LEDJMkWmgMWfmbgXg) |
| mb   | Mathias Behrle |          |
| kp   | Korbinian Preisler |          |
| cpm  | Carlos Perelló Marín |          |
| jfj  | Juan Fernando Jaramillo |          |
| ik   | Igor Támara |          |
| bch  | Bertrand Chenal |          |
| _nick_ | _add your name here_ |          |

## Testing Result Shortcuts ##
| Shortcut | Description                           |
|:---------|:--------------------------------------|
| tst      | Person is testing this topic          |
| ok       | Test was generally ok                 |
| nok      | Test was broken (note roundup issues) |
| -        | Module did not have this functionality|

# Release #

## Installation on different operating systems ##
| Package | Linux | Windows | Mac OSX | Other |
|:--------|:------|:--------|:--------|:------|
| Client  | us:ok |         |         |
| Server  | us:ok |         |         |
| Neso    | us:ok |         |         |

## Server ##

| Function | Actions | Workflows | Reports | de | en | es | fr | Issues |
|:---------|:--------|:----------|:--------|:---|:---|:---|:---|:-------|
| ir       | us:tst, |           |         |    |    |    |    |        |
| res      | us:ok   |           |         |    |    |    |    |        |
| workflow | us:ok   |           |         |    |    |    |    |        |
| webdav   | us:ok,  |           |         |    |    |    |    | 1212   |
| sqlite   | us:ok   |           |         |    |    |    |    |        |

## Client ##

| de | en | es | fr | Issues |
|:---|:---|:---|:---|:-------|
| us:ok | us:ok |    |    |        |

## Neso ##
| General |
|:--------|
|         |

## Estimated Modules Release Date 2009-10-19 ##
Planned Modules Release Date 2009-10-19

| Module | Actions | Workflows | Reports | de | en | es | fr | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:-------|
| account | us:ok   | us:ok     | us:ok   | us:ok | us:ok |    |    |        |
| account\_be |         |           |         |    |    |    |    |        |
| account\_de\_skr03 | us:ok   | -         | -       |    |    | -  | -  |        |
| account\_invoice  | us:ok   | us:ok     | us:ok   | us:ok | us:ok |    |    |        |
| account\_invoice\_history | us:ok   | -         | -       | us:ok | us:ok |    |    |        |
| account\_invoice\_line\_standalone | us:ok   |           |         |    |    |    |    |        |
| account\_product  | us:ok   | -         | -       | us:ok | us:ok |    |    |        |
| account\_statement | us:ok   | us:ok     | -       | us:ok |    |    |    |        |
| analytic\_account |         | -         | -       |    |    |    |    |        |
| analytic\_invoice |         | -         | -       |    |    |    |    |        |
| analytic\_purchase  |         | -         | -       |    |    |    |    |        |
| analytic\_sale  |         | -         | -       |    |    |    |    |        |
| calendar  | us:ok, mb:tst | -         | -       | us:ok | us:ok |    |    | see also http://spreadsheets.google.com/ccc?key=tcP37m3wxUAUC_pxct2xYqQ&hl=en |
| calendar\_todo  | us:ok, mb:tst | -         | -       | us:ok | us:ok |    |    | see also http://spreadsheets.google.com/ccc?key=tcP37m3wxUAUC_pxct2xYqQ&hl=en |
| company  | us:ok   | -         | us:ok   | us:ok | us\_ok |    |    |        |
| company\_work\_time |         | -         |         |    |    |    |    |        |
| country  | us:ok   | -         | -       | us:ok | us:ok |    |    |        |
| currency | us:ok   | -         | -       | us:ok | us:ok |    |    |        |
| google\_maps | us:ok   | -         | -       | us:ok | us:ok |    |    |        |
| google\_translate |         |           |         |    |    |    |    |        |
| ldap\_authentification |         |           |         |    |    |    |    |        |
| ldap\_connection |         |           |         |    |    |    |    |        |
| party  | us:ok   | -         | us:ok   | us:ok | us:ok |    |    |        |
| party\_vcarddav | us:ok, mb:tst | -         | -       | us:ok | us\_ok |    |    | see also http://spreadsheets.google.com/ccc?key=tcP37m3wxUAUC_pxct2xYqQ&hl=en |
| product | us:ok   | -         | us:ok   | us\_ok | us\_ok |    |    |        |
| product\_cost\_fifo | us:ok   | -         | -       | us:ok | us:ok |    |    |        |
| product\_cost\_history | us:ok   | -         | us:ok   |    | us:ok |    |    |        |
| product\_price\_list | us:ok   | -         | -       | us:ok | us:ok |    |    | ~~1151~~ |
| project\_plan |         |           |         |    |    |    |    |        |
| project |         |           |         |    |    |    |    |        |
| project\_revenue |         |           |         |    |    |    |    |        |
| purchase  | us:ok,  | us:ok,    | us:ok,  | us:ok, | us:ok, |    |    |        |
| purchase\_invoice\_line\_standalone |         |           |         |    |    |    |    |        |
| sale   | us:ok   | us:ok     | us:ok   | us:ok |us:ok |    |    |        |
| sale\_price\_list | us:ok   | -         | -       | us:ok | us:ok |    |    | 1252   |
| stock  | us:ok,  | us:ok,    | us:ok,  | us:ok | us:ok |    |    | 961,   |
| stock\_forecast | us:tst  |           |         |    |    |    |    |        |
| stock\_inventory\_location | us:ok   | us:ok     | -       | us\_ok | us:ok |    |    |        |
| stock\_location\_sequence | us:ok   | -         | -       | us:ok | us:ok |    |    |        |
| stock\_product\_location |         |           |         |    |    |    |    |        |
| stock\_supply  |         | -         | -       |    |    |    |    |        |
| stock\_supply\_day |         |           |         |    |    |    |    |        |
| timesheet |         |           |         |    |    |    |    |        |

(`*` not tested in detail)

# Modules scheduled for Release after 2009-10-20 #
Please do not waste time to test these modules until 2009-10-20.

## Modules on tryton.org ##

| Module | Actions | Workflows | Reports | de | en | es | fr | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:-------|
|        |         |           |         |    |    |    |    |        |

## External Modules waiting for Review ##

| Module | Actions | Workflows | Reports | de | en | es | fr | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:-------|
| [account\_invoice\_discount](http://mercurial.intuxication.org/hg/account_invoice_discount/) |         |           |         |    |    |    |    |        |
| [party\_bank](http://mercurial.intuxication.org/hg/party_bank/) |         |           |         |    |    |    |    |        |
| [party\_type](http://mercurial.intuxication.org/hg/party_type/) |         |           |         |    |    |    |    |        |
| [sale\_discount](http://mercurial.intuxication.org/hg/sale_discount/) |         |           |         |    |    |    |    |        |