# Ideas #

This page collects some development ideas that requires some attention before being planned on release.

  * Allow to use database users per users.
  * Allow to load external protocols.
  * Pass server name typed in the client to the database list function. It will allow to return custom database named based on server name.
  * ~~Create a WYSIWYG document editor integrated in the Tryton client.~~
  * ~~Improve report engine to allow to convert from any Ooo format to any Ooo format.~~
  * ~~Improve [search widget](http://groups.google.com/group/tryton-dev/browse_thread/thread/dce32732fde11375)~~
  * Create a module that adds history to ir.attachment and expose versions/revisions to WebDAV
  * Add a method on cursor to provide something like :

> `(ids[x:x + cursor.IN_MAX] for x in xrange(0, len(ids), cursor.IN_MAX))`

> And replace all current `cursor.IN_MAX` loops.
  * Add renderer for image in tree view with `CellRendererPixbuf`
  * Add `average` tag like the `sum` on list view.
  * ~~Use `*`.po format for module translation.~~
  * Look at [XDot](http://code.google.com/p/jrfonseca/wiki/XDot) to add a diagram visualization.
  * Make "active" field for logical deletion configurable on ModelStorage
  * Create a email to send queue. This will allow to include sending email in the cursor transaction.
  * Use [pysandbox](http://github.com/haypo/pysandbox) instead of custom safe\_eval
  * Write Tryton generator and consumer for [PyF](http://pyfproject.org/)
  * Replace [MPTT](http://en.wikipedia.org/wiki/MPTT) by [Closure Table](http://dirtsimple.org/2010/11/simplest-way-to-do-tree-based-queries.html?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed:+pje-on-programming+(PJE+on+Programming))