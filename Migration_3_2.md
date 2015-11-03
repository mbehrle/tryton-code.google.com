# Migration from 3.0 -> 3.2 #

## Must ##

  * Change all relates to use only active\_ids. See: http://codereview.tryton.org/3261002/diff/20001/trytond/modules/purchase/purchase.xml
  * Must adapt signature of "def write()". See: http://codereview.tryton.org/1641003/
  * Add index to one2many's on\_change add. See: http://hg.tryton.org/modules/account_invoice?cmd=changeset;node=01c2f7174352
  * Replace set action in xxx2many fields . See: https://bitbucket.org/nantic/trytond-babi/commits/145b7108f452b8f8b703b498ee870185794f0e3b
  * Add new with\_on\_change parameter on default\_get. See: https://bitbucket.org/nantic/trytond-babi/commits/c7d3253d9be13e0989138102da0d060aa2c58afa
  * If sale or purchase is installed, account\_invoice\_stock must be installed on update with -i account\_invoice\_stock


## Should ##

  * Remove main entry point in test scripts => test must be executed with trytond/tests/run-tests.py script
  * Import doctest\_dropdb from test\_tryton instead of define it in test script
  * Remove the insertion of 'trytond' in path in test script