

# Introduction #

Using Tryton code as a library can be useful for various stuff:
  * Testing/discovering without having to interact with the GUI.
  * Importing non-trivial or huge data.
  * Easily provide a new interface to Tryton.

Of course this list is not extensive.

# Example #

This example does the following things:
  * Import trytond code.
  * Populate the pool of models (the one that is used all over the modules to do the `self.pool.get('model.name')`.
  * Create a new party (so this example will only work with databases where the party module is already installed).
  * Print this new party id.
  * Commit the db transaction.

Notes:
  * The Tryton server path must be present on your [Python path](http://docs.python.org/using/cmdline.html#envvar-PYTHONPATH). On Linux you can add something like `export PYTHONPATH=/path/to/trytond/:$PYTHONPATH` in your .bashrc.
  * It's possible to do safe/harmless tests just by avoiding to the `cursor.commit()` call.
  * If an instance of trytond is already running for this db, it's possible that the cache becomes unsynced (because of the change you do from your script). A way to avoid this is to provide `multi_server = True` in the config file of the server (but it will slow down the cache mechanisms).
  * This kind of script makes very easy to profile Tryton and/or custom modules with the [profiling tools of Python](http://docs.python.org/library/profile.html).
  * Ensure that you manage the cursor. Eg. Changes will be committed to the database only after a cursor.commit() is issued.
### Version 2.8 ###
```
#!/usr/bin/python
# -*- coding: iso-8859-1 -*-

import os,sys
DIR = os.path.abspath(os.path.normpath(os.path.join(__file__,
    '/', 'usr', 'lib', 'python2.6', 'site-packages', 'trytond')))#Replace with your path
if os.path.isdir(DIR):
    sys.path.insert(0, os.path.dirname(DIR))
    
from trytond.config import CONFIG
# Load the configuration file
CONFIG.update_etc('/etc/trytond.conf')# Replace with your path
from trytond.pool import Pool
#from trytond.model import Cache
from trytond.cache import Cache
from trytond.transaction import Transaction

# dbname contains the db you want to use
dbname = 'test'
CONTEXT={}

Pool.start()
pool = Pool(dbname)

# Clean the global cache for multi-instance
Cache.clean(dbname)

# Instantiate the pool
with Transaction().start(dbname, 0, context=CONTEXT):
    pool.init()

# User 0 is root user. We use it to get the admin id:
with Transaction().start(dbname, 0, context=CONTEXT):
    user_obj = pool.get('res.user')
    user = user_obj.search([('login', '=', 'admin')], limit=1)[0]
    user_id = user.id

with Transaction().start(dbname, user_id, context=CONTEXT) as transaction:
    # No password is needed, because we are working directly with the
    # API, bypassing any networking stuff.
    # don't forget to install the party's module before this test.
    party_obj = pool.get('party.party')
    new_party = party_obj.create([{'name': 'New party'}])[0]
    new_party_id = new_party.id
    transaction.cursor.commit()

print new_party_id
# Reset the global cache for multi-instance
Cache.resets(dbname)
```
### Version 2.2 ###
```
#!/usr/bin/python
# -*- coding: iso-8859-1 -*-
import os,sys
DIR = os.path.abspath(os.path.normpath(os.path.join(__file__,
    '/', 'usr', 'local', 'tryton', 'trytond', 'trytond')))
if os.path.isdir(DIR):
    sys.path.insert(0, os.path.dirname(DIR))
    
from trytond.config import CONFIG
# Load the configuration file
CONFIG.update_etc('/usr/local/tryton/trytond/etc/trytond.conf')# Replace with your path
from trytond.pool import Pool
from trytond.model import Cache
from trytond.transaction import Transaction

# dbname contains the db you want to use
dbname = 'dbTryton'
CONTEXT={}

Pool.start()
pool = Pool(dbname)

# Clean the global cache for multi-instance
Cache.clean(dbname)

# Instantiate the pool
with Transaction().start(dbname, 0, context=CONTEXT):
    pool.init()

# User 0 is root user. We use it to get the admin id:
with Transaction().start(dbname, 0, context=CONTEXT):
    user_obj = pool.get('res.user')
    user = user_obj.search([('login', '=', 'admin')], limit=1)[0]

with Transaction().start(dbname, user, context=CONTEXT) as transaction:
    # No password is needed, because we are working directly with the
    # API, bypassing any networking stuff.
    # don't forget to install the party's module before this test.
    party_obj = pool.get('party.party')
    new_party_id = party_obj.create({'name': 'New party'})
    transaction.cursor.commit()

print new_party_id
# Reset the global cache for multi-instance
Cache.resets(dbname)
```
### Version 1.8 ###
```
#! /usr/bin/env python
from trytond.config import CONFIG
from trytond.modules import register_classes
from trytond.pool import Pool
from trytond.backend import Database
from trytond.model import Cache
from trytond.transaction import Transaction

# Load the configuration file
CONFIG.configfile = '/etc/trytond.conf'   # Replace with your path
CONFIG.load()

# Register classes populates the pool of models:
register_classes()

# dbname contains the db you want to use
DBNAME = 'test'
# Instantiate the database and the pool
DB = Database(DBNAME).connect()
POOL = Pool(DBNAME)
POOL.init()

# Clean the global cache for multi-instance
Cache.clean(DBNAME)

# User 0 is root user. We use it to get the admin id:
with Transaction().start(DBNAME, 0, None):
    user_obj = POOL.get('res.user')
    user = user_obj.search([('login', '=', 'admin')], limit=1)[0]

with Transaction().start(DBNAME, user, None) as transation:
    # No password is needed, because we are working directly with the
    # API, bypassing any networking stuff.
    party_obj = POOL.get('party.party')
    new_party_id = party_obj.create({'name': 'New party'})
    transaction.cursor.commit()

print new_party_id

# Reset the global cache for multi-instance
Cache.resets(DBNAME)
```

### Version 1.6 ###

```
#! /usr/bin/env python
import sys, os
import logging
logging.basicConfig(level=logging.FATAL)

from trytond.config import CONFIG
CONFIG.load()
from trytond.modules import register_classes
from trytond.pool import Pool
from trytond.backend import Database
from trytond.tools import Cache

# Register classes populates the pool of models:
register_classes()

# dbname contains the db you want to use
DBNAME = 'test'
# Instantiate the database and the pool
DB = Database(DBNAME).connect()
POOL = Pool(DBNAME)
POOL.init()

# Get a cursor on the database
cursor = DB.cursor()
# Clean the global cache for multi-instance
Cache.clean(DBNAME)

# User 0 is root user. We use it to get the admin id:
user_obj = POOL.get('res.user')
user = user_obj.search(cursor, 0, [
        ('login', '=', 'admin'),
        ], limit=1)[0]

# No password is needed, because we are working directly with the
# API, bypassing any networking stuff.
party_obj = POOL.get('party.party')
new_party_id = party_obj.create(cursor, user, {
        'name': 'New party'
        })
print new_party_id

cursor.commit()
cursor.close()
# Reset the global cache for multi-instance
Cache.resets(DBNAME)

```