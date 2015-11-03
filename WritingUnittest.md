

# Introduction #

Tryton provides a unit testing framework based on [unittest](http://docs.python.org/library/unittest.html). The goal is to be able to test any function of any Model defined in this module and prevent regression during development.

It is possible to run tests under [coverage](http://pypi.python.org/pypi/coverage) to verify the coverage of the unit tests.

Those tests are run each day on Tryton test server for each database backend. You can find results [here](http://tests.tryton.org/~test/).

# Running tests #

When running unittest, Tryton will create a temporary database with this form `test_12345` where the number is the current time in seconds since the Epoch, except for sqlite backend where it uses a memory database.

Tryton will read the database type to use from the configuration file with SQLite as default value because SQLite in memory database is faster.

## From trytond ##

It is possible to run tests for all installed modules with this command:

`python trytond/tests/test_tryton.py --modules`

## From setup.py ##

To run tests when installing a module:

`python setup.py test`

## From command line ##

`python trytond/modules/module_name/tests/test_module_name.py`


# Files #

Here is the minimal files required to define unit test.


---

`module_name/`<br />
> `setup.py`<br />
> `tests/`<br />
> > `__init__.py`<br />
> > `test_module_name.py`<br />

---


## `setup.py` ##

The setup parameters to pass to setup of setuptools to allow to [run tests when building the package](http://peak.telecommunity.com/DevCenter/setuptools#test-build-package-and-run-a-unittest-suite):

```
setup(
    ...
    packages=[
       ...
       'trytond.modules.module_name.tests',
    ],
    ...
    test_suite='tests',
    test_loader='trytond.test_loader:Loader',
)
```

## `tests/__init__.py` ##

The tests module must have a function named `suite` that will return the unittest suite for the module. This function will be called by `trytond.test_loader:Loader`. Generally this function is defined in `test_module_name.py` so the file looks like:

```
   from test_module_name import suite
```

## `tests/test_module_name.py` ##

This is the core file that will define the unittest. This file could be run directly with `python trytond/modules/module_name/tests/test_module_name.py`.
Here is a template of this file:

```
#!/usr/bin/env python

import sys, os
DIR = os.path.abspath(os.path.normpath(os.path.join(__file__,
    '..', '..', '..', '..', '..', 'trytond')))
if os.path.isdir(DIR):
    sys.path.insert(0, os.path.dirname(DIR)) # Add trytond to Python path

import unittest
import trytond.tests.test_tryton
# Retrieve some common useful object:
# POOL is the Pool that contains Tryton Models for the test database
# DB is the Database object that handle the connection to the test database
# USER is the id of the 'admin' user
# CONTEXT is the context
from trytond.tests.test_tryton import POOL, DB, USER, CONTEXT


class ModuleNameTestCase(unittest.TestCase): # Define a TestCase class for the module

    def setUp(self):
        trytond.tests.test_tryton.install_module('module_name') # Install the module

    # Define test functions according to TestCase Objects

def suite():
    suite = trytond.tests.test_tryton.suite()
    # Add external tests on which this module dependents
    suite.addTests(unittest.TestLoader().loadTestsFromTestCase(ModuleNameTestCase)) # Add tests from module TestCase.
    # Add any other tests from this module
    return suite

if __name__ == '__main__':
    unittest.TextTestRunner(verbosity=2).run(suite()) # Run tests if run as a script
```

Test functions must manage their own cursor and transaction like this:
```
cursor = DB.cursor()
...
cursor.commit() # or cursor.rollback()
cursor.close()
```