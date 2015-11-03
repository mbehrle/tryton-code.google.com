**#summary Migration 3.2 -> 3.4**

# Migration from 3.2 -> 3.4 #

## Must ##

  * Remove with\_on\_change parameter from default\_get. See http://hg.tryton.org/trytond/rev/a26fa53ada28
  * Use new configuration file format, see http://doc.tryton.org/3.4/trytond/doc/topics/configuration.html
  * trytond: `-i` parameter removed, arguments of `-u` must be separated by space.
  * `ldap_connection` module removed:
    * Run: `DELETE FROM ir_module_module WHERE name = 'ldap_connection'`
    * Configure `LDAP` connection using `trytond.conf` (See [doc](http://hg.tryton.org/modules/ldap_authentication/file/90f2551dea5a/doc/index.rst))
  * `account` module, fix the party field of `account.move.line` by running `modules/account/scripts/fix_party`

## Should ##

  * Replace `user=0` by `_check_access` in `context`
  * Use `grouped_slice helper`. See http://hg.tryton.org/trytond/rev/f00ae016f341
  * Use `doctest_setup/teardown`. See http://hg.tryton.org/modules/stock_supply/rev/0423d3d1f36f

## Take care ##

  * trytond
    * new argument `--all`: a new database can be initialized using `-u res ir` or `--all`. `all` isn't a valid argument for `-u` parameter.
    * new argument `--dev`: **auto-reload** of modules is only enabled in development mode (`SIGUSR1` can always be used in order to trigger a manual restart)
    * Logging configuration: logs can be configured using a configparser-format file, see http://doc.tryton.org/3.4/trytond/doc/topics/logs.html
  * [The trigger user should not more be needed](https://bugs.tryton.org/issue4278).