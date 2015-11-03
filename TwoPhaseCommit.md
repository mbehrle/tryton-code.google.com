# Introduction #

The [Two-Phase commit protocol](https://en.wikipedia.org/wiki/Two-phase_commit_protocol) (TPC) is an algorithm that coordinates distributed transactions.

# Details #

The Zope world have been using TPC for a long time due to the design of the
Zope Object Database. This Object-Oriented Database is stored as a huge file
somewhere on the filesystem and it provides ACID transactions. So as soon as
they needed to write in a relational database they were confronted to the
problem of distributed transactions.

In the end they have created a standalone python package implemeting the
protocol. The [documentation](http://zodb.readthedocs.org/en/latest/transactions.html) is a realy good introduction to the whole problem.

The main idea is that you have to implement so-called `DataManagers` for each
of your subsystem involved in the distributed transaction. They have defined an
interface that must be followed in order to interact gracefully with the
`transaction` module. Once all those datamanagers are registered into a
distributed transaction and voilà … all the transactions should succeed or fail
at the same time.

So it looks like the main difficulty is to implement `DataManagers`. The Zope
folks have already written some of them (although they are not separated from
other zope functionnalities):

  * **email**: https://pypi.python.org/pypi/zope.sendmail
  * **filesystem**: https://pypi.python.org/pypi/zope.file
  * **relational databases**: https://pypi.python.org/pypi/zope.rdb

I have also noticed that the Python DB API v2.0 provides
[an extension](http://www.python.org/dev/peps/pep-0249/#optional-two-phase-commit-extensions) for database connectors to implement the TPC. Unfortunately it
seems that only psycopg supports this extension. MySQL and SQLite lacks the
`idx()` methods defined in the extension (and does not raise the
`NotSupportedError` neither which is quite strange).

# Implementation #

To not being to intrusive and preformance killer, we should use the main transaction without tpc like explained in http://blogs.gnome.org/jamesh/2008/03/04/python-tpc/.

Other transaction (following the DataManager API) could be added to the Tryton transaction which will be commited using the tpc.

Then we have to replace the call to `commit` in `trytond/server.py` with a call to
`transaction.commit`.

A before and after commit hook could be added to complete the API.