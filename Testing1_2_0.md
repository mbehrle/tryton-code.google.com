

# Introduction #
This page is for collaborated testing. If you like to share your experience, just put your nickname and a results shortcut into the fields you tested. General its no problem when there are many people test the same thing, just put your results into the table, too. Try to test parts which are untested.
  * Test all Actions and Workflows in expected functionality.
  * Test if Reports functioning
  * Test Translations for:
    * de: German
    * en: English
    * es: Spanish
    * fr: French

If you find bugs, create for each bug an issue in [roundup](http://bugs.tryton.org/). Please collect the issue number in the column 'Issues'.

## Nicknames ##

| Nick | Name | Comments |
|:-----|:-----|:---------|
| us   | Udo Spallek |see some details of my [testing plan](http://spreadsheets.google.com/ccc?key=pKmfajjFuwcsmjMRqWyiRPw) |
| mb   | Mathias Behrle |          |
| kp   | Korbinian Preisler |          |
| cpm  | Carlos Perelló Marín |          |
| jfj  | Juan Fernando Jaramillo |          |
| ik   | Igor Támara |          |
| bch  | Bertrand Chenal |          |

## Testing Result Shortcuts ##
| Shortcut | Description                           |
|:---------|:--------------------------------------|
| tst      | Person is testing this topic          |
| ok       | Test was generally ok                 |
| nok      | Test was broken (note roundup issues) |
| -        | Module did not have this functionality|
# Release #

## Server ##

| Module | Actions | Workflows | Reports | de | en | es | fr | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:-------|
| ir     | mb:tst  |           |         | mb:ok  |    | ik:ok | bch:ok | 996    |
| res    | mb:tst  |           |         | mb:ok  |    | ik:ok | bch:ok  |        |
| workflow  | mb:tst  |           |         | mb:ok |    | ik:ok | bch:ok |        |
| webdav  | mb:tst, us:tst |           |         | mb:ok |    | ik:ok | bch:ok | 941    |

## Client ##

| de | en | es | fr | Issues |
|:---|:---|:---|:---|:-------|
| mb:ok |    |    | bch:ok |        |

## Estimated Modules Release Date 2009-04-20 ##
Planned Modules Release Date 2009-04-13 [postponed](postponed.md)

| Module | Actions | Workflows | Reports | de | en | es | fr | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:-------|
| account | kp:ok, us:ok`*`, cpm:ok, mb:tst | us:ok, cpm:ok | mb:ok, us:ok, cpm:ok | kp:ok, mb:ok | 591 |    | bch:ok | ~~916~~,917,~~919~~, ~~923~~, ~~978~~, ~~986~~, ~~990~~ |
| account\_invoice\_history | kp:ok, us:ok, cpm:ok | -         | -       | mb:ok |    |    | bch:ok | ~~977~~ |
| account\_invoice  | us:ok,cpm:ok | us:ok     | us:ok,cpm:ok,kp:ok | mb:ok  |    |    | bch:ok | ~~994~~, ~~1005~~ |
| account\_product  | us:ok,cpm:ok | -         | -       | mb:ok |    |    | bch:ok |        |
| account\_statement | us:ok   | us:ok     | -       | mb:ok |    |    | bch:ok | ~~984~~ |
| analytic\_account | kp:ok,us:ok`*` | -         | -       | mb:ok |    |    | bch:ok | ~~992~~ |
| analytic\_invoice | kp:ok,us:ok`*` | -         | -       | mb:ok |    |    | bch:ok | ~~992~~ |
| analytic\_purchase  | kp:ok   | -         | -       | mb:ok |    |    | bch:ok | ~~993~~ |
| analytic\_sale  | kp:ok   | -         | -       | mb:ok |    |    | bch:ok | ~~993~~ |
| company  | us:ok   | -         | us:ok   | mb:ok |    | jfj:ok | bch:ok |        |
| country  | us:ok   | -         | -       | mb:ok |    | jfj:ok | bch:ok | ~~1001~~ |
| currency | us:ok   | -         | -       | mb:ok |    | jfj:ok | bch:ok | ~~1000~~, ~~1012~~ |
| google\_maps | us:ok   | -         | -       | mb:ok |    |    | bch:ok |        |
| party  | us:ok,cpm:ok | -         | us:ok   | mb:ok |    | jfj:ok | bch:ok |        |
| product | us:ok,cpm:ok | -         | us:ok   | mb:ok |    | jfj | bch:ok |        |
| purchase  | kp:ok,us:ok | kp:ok     | kp:ok   | mb:ok |    | jfj | bch:ok | ~~703~~, ~~991~~ |
| sale   | us:ok,kp:ok | us:ok     | us:ok,kp:ok | mb:ok |    | jfj | bch:ok | ~~985~~, ~~703~~, ~~991~~ |
| stock  | kp:ok,us:ok | us:ok     | us:ok,mb:ok | mb:ok |    | jfj | bch:ok | ~~928~~, ~~929~~, 1006 |
| stock\_location\_sequence | kp:ok,us:ok | -         | -       | mb:ok |    |    | bch:ok |        |
| stock\_supply  | kp:ok,us:ok | -         | -       | mb:ok |    |    | bch:ok |        |

(`*` not tested in detail)

# Modules scheduled for Release after 2009-04-20 #
Please do not waste time to test these modules until 2009-04-20.

## Modules on tryton.org ##

| Module | Actions | Workflows | Reports | de | en | es | fr | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:-------|
| account\_be |         |           |         |    |    |    |    |        |
| account\_de\_skr03 |         |           |         | mb:ok |    |    |    | ~~1016~~, ~~1025~~|
| ~~google\_translate~~ |         |           |         | mb:ok |    |    | bch:ok |        |
| product\_cost\_fifo |         |           |         |    |    |    |    |        |
| product\_cost\_history |         |           |         |    |    |    |    |        |
| ~~project~~ |         |           |         | mb:ok |    |    | bch:ok |        |
| ~~project\_revenue~~ |         |           |         | mb:ok |    |    | bch:ok |        |
| stock\_forecast |         |           |         |    |    |    |    |        |
| stock\_inventory\_location |         |           |         |    |    |    |    |        |
| stock\_product\_location |         |           |         |    |    |    |    |        |
| stock\_supply\_day |         |           |         |    |    |    |    |        |
| ~~timesheet~~ |         |           |         | mb:ok |    |    | bch:ok |        |

## External Modules ##

| Module | Actions | Workflows | Reports | de | en | es | fr | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:-------|
| [account\_invoice\_discount](http://mercurial.intuxication.org/hg/account_invoice_discount/) | mb:ok   |           | mb:ok   | mb:ok |    |    |    |        |
| [party\_bank](http://mercurial.intuxication.org/hg/party_bank/) | mb:ok   |           |         | mb:ok |    |    |    |        |
| [party\_type](http://mercurial.intuxication.org/hg/party_type/) | mb:ok   |           |         | mb:ok |    |    |    |        |
| [sale\_discount](http://mercurial.intuxication.org/hg/sale_discount/) | mb:ok   |           | mb:ok   | mb:ok |    |    |    | ~~1055~~ |