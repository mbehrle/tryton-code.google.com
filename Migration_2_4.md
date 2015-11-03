# Migration from 2.2 -> 2.4 #

## MUST ##

  * `[XML]` Replace nested view by reference id
    * Examples: http://hg.tryton.org/trytond/rev/49085a518188
  * `[XML]` Replace `fill` attribute by `expand`
    * Explanation & examples: http://hg.tryton.org/trytond/rev/79960df16ff5
  * `[PY]` New wizard design
    * Examples: http://hg.tryton.org/trytond/rev/12cb56cc422a
  * `[PY]` NULL value is None and not False
    * Examples: http://hg.tryton.org/trytond/rev/30afefa8da0e http://hg.tryton.org/trytond/rev/3e12e07af677
  * `[PY][XML]` Simplify workflow engine
    * Example: http://hg.tryton.org/modules/account_invoice/rev/48de813ee9ac
    * trytond commit: http://hg.tryton.org/trytond/rev/49085a518188

## Take care ##

  * **Database: default value for Integer, Float and Numeric changed** ( http://hg.tryton.org/trytond/rev/3e12e07af677 ). With tryton 2.2, default value in database for Integer, Float and Numeric fields is 0. With tryton 2.4, default value in database for Integer, Float and Numeric fields is NULL. The following integer field:
```
test_int = fields.Integer(string = u"blabla", required = False, readonly = False)
```
    * generate this DDL with tryton 2.2:
```
ALTER TABLE "modulename" ADD COLUMN "test_int" int4
COMMENT ON COLUMN "modulename"."test_int" IS 'blabla'
ALTER TABLE "modulename" ALTER COLUMN "test_int" SET DEFAULT 0
ALTER TABLE "modulename" ALTER COLUMN "test_int" SET NOT NULL
```
    * generate this DDL with tryton 2.4:
```
ALTER TABLE "modulename" ADD COLUMN "test_int" int4
COMMENT ON COLUMN "modulename"."test_int" IS 'blabla'
ALTER TABLE "modulename" ALTER COLUMN "test_int" SET DEFAULT NULL
```