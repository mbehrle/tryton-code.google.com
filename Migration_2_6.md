# Migration from 2.4 -> 2.6 #

## MUST ##

  * `[PY]` Active Record
    * All steps here: http://www.b2ck.com/~ced/active_record_migration.txt
      * Define all in each python file
      * Replace class instance by Pool.register in init.register() using the same order
      * Remove `_description`
      * Rename `_name` into `__name__`
      * Replace `__init__` by `__setup__`
        * Rename `_rpc` into `__rpc__` and use RPC as value
        * Remove `_reset_columns`
      * Replace init by `__register__`
      * Replace default\_xxx method by `classmethod` or `staticmethod` (depending if it uses `self/cls`)
      * Change constraint methods into classmethod with records as input or instance method
      * Change on\_change, `on_change_with`, autocomplete into instance method without values
      * Change getter into:
        * instance method that just return value
        * `classmethod` with records that return a dict with values
      * Change setter into `classmethod` with records
      * Rename xxx\_obj into Xxx
      * browse takes only list of ids, for int just instanciate the `Model`
      * create return a instance
      * write, delete are `classmethod` with list of instance and return nothing
      * read takes only list of ids, for int use this: `value, = cls.read([id])`
      * `copy` is a `classmethod` that takes only a list of instance and return a list of instance
      * Replace `session` from wizard method by `self`
      * Use `PoolMeta` for extending `Model`
      * Cache method is replaced by a Cache instance on the class
      * Methods to simply replace by `classmethod`:
        * `search_rec_name`
      * Methods to replace by classmethod with records:
        * `check_xml_record`
      * search returns list of instance
    * Example: http://hg.tryton.org/modules/party/rev/505cc38cf2f2
  * `[PY]` `__tryton__.py` replaced with `tryton.cfg`
    * Example: http://hg.tryton.org/modules/party/rev/42528756c4bf