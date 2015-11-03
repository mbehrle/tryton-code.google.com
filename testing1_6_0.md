

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
    * ru: Russian
    * _add your language here_

If you find bugs, create for each bug an issue in [roundup](http://bugs.tryton.org/). Please collect the issue number in the column 'Issues'.

## Nicknames ##

| Nick | Name | Comments |
|:-----|:-----|:---------|
| us   | Udo Spallek |          |
| mb   | Mathias Behrle |          |
| kp   | Korbinian Preisler |          |
| cpm  | Carlos Perelló Marín |          |
| jfj  | Juan Fernando Jaramillo |          |
| ik   | Igor Támara |          |
| bch  | Bertrand Chenal |          |
| tp   | Tobias Paepke |          |
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
| Client  | us:ok |         | tp:ok   |
| Server  | us:ok |         |         |
| Neso    | us:ok |         |         |

## Server ##

| Function | Actions | Workflows | Reports | de | en | es | fr | ru | Issues |
|:---------|:--------|:----------|:--------|:---|:---|:---|:---|:---|:-------|
| ir       |         |           |         |    |    |    |    |    | |
| res      |         |           |         |    |    |    |    |    |        |
| workflow |         |           |         |    |    |    |    |    |        |
| webdav   |         |           |         |    |    |    |    |    |        |
| sqlite   |         |           |         |    |    |    |    |    |        |

## Client ##

| de | en | es | fr | ru |Issues |
|:---|:---|:---|:---|:---|:------|
| us:ok | us:ok |    |    |    |       |

## Neso ##
| General |
|:--------|
|         |

## Estimated Modules Release Date 2010-05-03 ##

| Module | Actions | Workflows | Reports | de | en | es | fr | ru | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:---|:-------|
| account | us:ok   | us:ok     | us:ok   | us:ok | us:ok |    |    |    |        |
| account\_be |         |           |         |    |    |    |    |    |        |
| account\_de\_skr03 | us:ok   | -         | -       |    |    | -  | -  |    |        |
| account\_invoice  | us:ok   | us:ok     | us:ok   | us:ok | us:ok |    |    |    |        |
| account\_invoice\_history | us:ok   | -         | -       | us:ok | us:ok |    |    |    |        |
| account\_invoice\_line\_standalone |         |           |         |    |    |    |    |    |        |
| account\_product  | us:ok   | -         | -       | us:ok | us:ok |    |    |    |        |
| account\_statement |         |           | -       |    |    |    |    |    |        |
| analytic\_account |         | -         | -       |    |    |    |    |    |        |
| analytic\_invoice |         | -         | -       |    |    |    |    |    |        |
| analytic\_purchase  |         | -         | -       |    |    |    |    |    |        |
| analytic\_sale  |         | -         | -       |    |    |    |    |    |        |
| calendar  | tp:ok   | -         | -       | tp:ok | tp:ok |    |    |    | see also http://spreadsheets.google.com/ccc?key=tcP37m3wxUAUC_pxct2xYqQ&hl=en |
| calendar\_scheduling  | mb:tst  | -         | -       | mb:ok | mb:ok |    |    |    | see also http://spreadsheets.google.com/ccc?key=tcP37m3wxUAUC_pxct2xYqQ&hl=en |
| calendar\_todo  | tp:ok   | -         | -       | tp:ok | tp:ok |    |    |    | see also http://spreadsheets.google.com/ccc?key=tcP37m3wxUAUC_pxct2xYqQ&hl=en |
| company  | us:ok   | -         | us:ok   | us:ok | us\_ok |    |    |    |        |
| company\_work\_time |         | -         |         |    |    |    |    |    |        |
| country  | us:ok   | -         | -       | us:ok | us:ok |    |    |    |        |
| currency | us:ok   | -         | -       | us:ok | us:ok |    |    |    |        |
| google\_maps | us:ok   | -         | -       | us:ok | us:ok |    |    |    |        |
| google\_translate |         |           |         |    |    |    |    |    |        |
| ldap\_authentification | tp:ok   | -         | -       | tp:ok | tp:ok |    |    |    | tested: openldap, Win2003 SBS |
| ldap\_connection | tp:ok   | -         | -       | tp:ok | tp:ok |    |    |    | tested: openldap, Win2003 SBS |
| party  | us:ok   | -         | us:ok   | us:ok | us:ok |    |    |    |        |
| party\_vcarddav |         | -         | -       |    |    |    |    |    | see also http://spreadsheets.google.com/ccc?key=tcP37m3wxUAUC_pxct2xYqQ&hl=en |
| product | us:ok   | -         | us:ok   | us\_ok | us\_ok |    |    |    |        |
| product\_cost\_fifo | us:ok   | -         | -       |    |    |    |    |    | ~~1523~~ |
| product\_cost\_history | us:ok   | -         |         |    |    |    |    |    |        |
| product\_price\_list |         | -         | -       |    |    |    |    |    |        |
| project\_plan |         |           |         |    |    |    |    |    |        |
| project | kp:ok   | -         | -       | kp:ok |    |    |    |    |        |
| project\_revenue | kp:ok   | -         | -       | kp:ok |    |    |    |    |        |
| purchase  | us:ok   | us:ok     | us:ok   |    |    |    |    |    |        |
| purchase\_invoice\_line\_standalone |         |           |         |    |    |    |    |    |        |
| sale   | us:ok   | us:ok     | us:ok   |    |    |    |    |    | ~~1529~~|
| sale\_price\_list |         | -         | -       |    |    |    |    |    |        |
| stock  | us:ok   | us:ok     | us:ok   |    |    |    |    |    |        |
| stock\_forecast |         |           |         |    |    |    |    |    |        |
| stock\_inventory\_location |         |           | -       |    |    |    |    |    |        |
| stock\_location\_sequence |         | -         | -       |    |    |    |    |    |        |
| stock\_product\_location |         |           |         |    |    |    |    |    |        |
| stock\_supply  |         | -         | -       |    |    |    |    |    |        |
| stock\_supply\_day |         |           |         |    |    |    |    |    |        |
| timesheet | kp:ok   | -         | kp:ok   | kp:ok |    |    |    |    |        |

(`*` not tested in detail)

# Modules scheduled after Release #
Please do not waste time to test these modules until the release named above.

## Modules on tryton.org ##

| Module | Actions | Workflows | Reports | de | en | es | fr | ru | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:---|:-------|
|        |         |           |         |    |    |    |    |    |        |

## External Modules waiting for Review ##

| Module | Actions | Workflows | Reports | de | en | es | fr | ru | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:---|:-------|
|        |         |           |         |    |    |    |    |    |        |