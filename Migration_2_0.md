# Migration from 2.0 -> 2.1 #

## MUST ##

  * `[XML]` Fix for new cron design
    * Examples: http://codereview.tryton.org/36004/
    * With ``gvim -p `find . -type f -name "*.xml" -exec grep -sl "record model=\"ir.cron\"" {} \;``` do the following changes:
      * Rename fields:
        * numbercall --> number\_calls
        * doall --> repeat\_missed
        * nextcall --> next\_call
      * Remove field:
        * priority
      * Change entries for cron users:
        * Set res.user executing a cron job to active False:
        * `<field name="active" eval="False"/>`

  * `[PY]` Change Pool into a Singleton
    * Examples:
      * http://codereview.tryton.org/42001
    * Add manually:
      * ``gvim -p `find . -type f -name "*.py" -exec grep -sl "self.pool.get" {} \;```
      * `find . -type f -name "*.py" -exec sed -i 's/self.pool.get/Pool().get/g' {} \;`
      * Add "from trytond.pool import Pool" to affected files.

  * `[PY]` Remove support of Python2.5 and fix py3 warnings
    * Examples:
      * http://hg2.tryton.org/modules/account/rev/8d50c3b2ed8f
    * Remove:
      * `from __future__ import with_statement`
    * Change setup.py :
      * `find . -type f -name "*.py" -exec sed -i '/from __future__ import with_statement/d' {} \;`

  * `[XML]` New Search Widget
    * Examples:
      * http://codereview.tryton.org/95002/
      * http://codereview.tryton.org/103001/
    * Remove per module all `select=  *` in xml:
      * `find . -type f -name "*.xml" -exec sed -i 's/.select="1"//g' {} \;`

  * `[PY]``[XML]` Use function name in workflow instead of python code
    * Examples:
      * http://hg.tryton.org/modules/account_invoice/rev/0fedf073bbe8

  * `[PY]` Improve Binary fields
    * Examples:
      * http://hg.tryton.org/modules/account_invoice/rev/399c7cfc01ca
    * Later fixes for migrion code:
      * base64.decodestring doesn't support buffer for [issue2295](https://code.google.com/p/tryton/issues/detail?id=2295)
        * http://codereview.tryton.org/181002/
      * trytond: StringIO doesn't like buffer for [issue2296](https://code.google.com/p/tryton/issues/detail?id=2296)
        * http://codereview.tryton.org/171006/
      * Fixing binary encoding and missing import in report migration
        * Examples:
          * https://bugs.tryton.org/issue2354
          * http://codereview.tryton.org/213002/

  * `[XML]` Update Reference fields from 0 to -1
    * Examples:
      * http://hg.tryton.org/modules/account/rev/e3579adcc619

  * `[PY]` Fix domain concatenation between list and tuple for JSON
    * Examples:
      * http://hg.tryton.org/modules/party/rev/0f2b1b61f544
      * http://hg.tryton.org/modules/account/rev/2753ca6d96dd

  * `[PY]` icons is not a module
    * Examples:
      * http://hg.tryton.org/modules/party/rev/5b2052739346
      * http://codereview.tryton.org/106001/

  * `[PY]` Set Tryton classifier
    * Examples
      * http://hg.tryton.org/modules/account/rev/f6ac373f7170
      * `find . -name "setup.py" -exec sed -i "s/        'Environment :: Plugins',/        'Environment :: Plugins',\n        'Framework :: Tryton',/" {} \;`

  * `[PY]` Set Python classifier
    * Set specific classifiers in setup.py for Python:
      * 'Programming Language :: Python :: 2.6',
      * 'Programming Language :: Python :: 2.7',
      * `find . -name "setup.py" -exec sed -i "s/        'Programming Language :: Python',/        'Programming Language :: Python :: 2.6',\n        'Programming Language :: Python :: 2.7',/" {} \;`

  * `[PY]` Instanciate Pool() into a variable for more than two uses per method
    * ``gvim -p `find . -type f -name "*.py" -exec pcregrep -Msl 'Pool.  *\n.  *Pool.  *\n.  *Pool' {} \;` ``
    * for each file in vim:
      * `/'Pool.  *\n.  *Pool.  *\n.  *Pool'`
      * and change manually

  * `[XML]` Remove support of Many2Many field in record XML
    * Examples:
      * http://hg.tryton.org/2.2/modules/account/rev/838330f48b9a
      * http://codereview.tryton.org/35005/patch/10003/12019
      * http://codereview.tryton.org/35005
    * Create separate records for group permissions:
      * `grep "'add', ref"   *.xml`


## MUST (seperate all in one shot) ##

  * `[CSV]``[PO]` replace .csv by .po file for translations
    * Examples:
      * http://hg.tryton.org/modules/account/rev/94373fe5722c

## MUST ##

  * Change format of search\_value on ir.action.act\_window(?)

  * Remove tabpos attribute on notebook

  * Add readonly on Transaction(?)

  * Rename expand and fill attributes into yexpand and yfill

  * Fix fields\_view\_get for new method signature

## SHOULD (Postmigration) ##

  * `[XML]` Remove 'New' menu entries

  * `[XML]` Remove "Management" from menu entries

  * `[XML]` Remove separator on top of Many2Many
    * Examples:
      * http://hg.tryton.org/modules/account_invoice/rev/4b238713adf8

  * `[PY]` Add test for depends
    * Examples:
      * http://hg.tryton.org/modules/account/rev/7a2a94d71d26

  * `[XML]` Check trigger permissions for all models
    * s.a. `[XML]` Remove support of Many2Many field in record XML

## CLEANUP ##

  * `[PO]` Clean all translations

  * `[XML]` Rework all views being displayed differently:
    * some fields are displayed with smaller size

## NOT MANDATORY ##

  * `[PY]` Make PYSON more Pythonic
    * Examples:
      * http://hg.tryton.org/modules/account/rev/cebf2de2baa2