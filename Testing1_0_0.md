

# Introduction #
This page is for collaborated testing. If you like to share your experience, just put your nickname and a results shortcut into the fields you tested. General its no problem when there are many people test the same thing, just put your results into the table, too. Try to test parts which are untested.
  * Test all Actions and Workflows in expected functionality.
  * Test if Reports functioning
  * Test Translations for:
    * de: German
    * en: English
    * es: Spanish
    * fr: French

If you find bugs, create for each bug an issue in roundup. Please collect the issue number in the column 'Issues'.

## Nicknames ##

| Nick | Name |
|:-----|:-----|
| us   | Udo Spallek |
| mb   | Mathias Behrle |
| kp   | Korbinian Preisler |

## Shortcuts ##
| Shortcut | Description                  |
|:---------|:-----------------------------|
| tst      | Person is testing this topic |
| ok       | Test was generally ok        |
| nok      | Test was broken (see issues) |

# Release #

## Server ##

## Client ##

## Modules Released 2008-11-17 ##

| Module | Actions | Workflows | Reports | de | en | es | fr | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:-------|
| account | us:ok   | us:ok     | us:ok   | mb:ok, us:ok |    |    |    |        |
| account\_invoice | us:ok   | us:ok     |         | mb:ok, us:ok (591) |591  |    |    |        |
| account\_product | us:ok   |           |         | mb:ok, us:ok |    |    |    |        |
| analytic\_account |         |           |         | mb:ok, us:ok |    |    |    |        |
| analytic\_invoice |         |           |         | mb:ok, us:ok |    |    |    |        |
| analytic\_purchase | kp:tst  |           |         | mb:ok, us:ok |    |    |    | ~~550~~ |
| analytic\_sale |         |           |         | mb:ok, us:ok |    |    |    |        |
| company | mb:ok, us:ok | mb:ok     | mb:ok   | mb:ok, us:ok |    |    |    | ~~533~~ |
| country | us:ok   | -         | -       | mb:ok, us:ok |    |    |    |        |
| currency | us:ok   | -         | -       | mb:ok, us:ok |    |    |    |        |
| google\_maps |us:ok    | -         | -       | mb:ok, us:ok |    |    |    |        |
| ir     |         |           |         | mb:ok, us:ok |    |    |    |        |
| party  | mb:tst,us:ok | mb:tst,us:ok | mb:ok us:ok | mb:ok:us:ok ~~(538)~~ |    |    |    | ~~533,(534)~~ |
| product | us:ok   |           |         | mb:ok, us:ok ~~(542,573)~~ |    |    |    | ~~545~~ |
| purchase | mb:tst,us:ok | mb:tst,us:ok | mb:tst,us:ok | mb:ok,us:ok |    |    |    | ~~536~~ |
| res    |         |           |         | mb:ok, us:ok |    |    |    |        |
| sale   | us:ok mb:tst | us:ok mb:tst | mb:tst  | mb:ok, us:ok |    |    |    | ~~545~~ |
| stock  | us:ok   | us:ok     | us:ok(some reports are untranslated) | us:ok (~~537~~,~~539~~),mb:ok  |    |    |    | ~~521~~, ~~541~~,~~543~~, ~~546~~, ~~556~~ |
| stock\_supply |kp:ok, us:ok |           |         | mb:ok, us:ok |    |    |    | ~~548~~, ~~554~~, ~~555~~|
| webdav | us:ok   | -         | -       | mb:ok, us:ok |    |    |    |        |
| workflow |         |           |         | mb:ok, us:ok |    |    |    |        |

# Modules not Relevant vor Release #
Please do not waste time to test this modules until 2008-11-17.

## Modules not Released on 2008-11-17 ##

| Module | Actions | Workflows | Reports | de | en | es | fr | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:-------|
| account\_statement | us:ok   |           |         | mb:ok, us:ok |    |    |    | Blocker:589 |
| project |         |           |         | mb:ok |    |    |    |        |
| project\_revenue |         |           |         | mb:ok |    |    |    |        |
| timesheet |         |           |         | mb:ok |    |    |    |        |

## External Modules ##
| Module | Actions | Workflows | Reports | de | en | es | fr | Issues |
|:-------|:--------|:----------|:--------|:---|:---|:---|:---|:-------|
| account\_de\_skr03\_2008 |         |           |         | mb:ok |    |    |    |        |