[![](http://code.google.com/images/GSoC2011_300x200.png)](http://code.google.com/soc/)


# Ideas #

Post your ideas for students during [Google's Summer of Code 2011](http://code.google.com/soc/) here. See the [FAQ entry](http://socghop.appspot.com/document/show/gsoc_program/google/gsoc2011/faqs#ideas) on the ideas list for further details.

## Easy ##

### Create a XPDL parser to load workflow ###
The Tryton server loads workflow with a specific XML format. It would be great to allow the server to parse [XPDL](http://en.wikipedia.org/wiki/XML_Process_Definition_Language) files to load the workflow in the database. Knowledge of XML and Python is required.

### Add full text search on records ###
[Full text search](http://en.wikipedia.org/wiki/Full_text_search) allows large amounts of text to be efficiently tokenized, indexed and searched. Full text search would be beneficial to users by giving them a powerful way to search records in Tryton. [Sphinx](http://www.sphinxsearch.com/) could be a good starting point. Knowledge of Python and SQL is required.

### Create a generic Django module to display Tryton models ###
Tryton has the capability to be used as a Python module. It could be useful to be able to display the models of Tryton into a [Django](http://www.djangoproject.com/) website. There is already an example of [POC](http://en.wikipedia.org/wiki/Proof_of_concept) on [TrytonDjango](TrytonDjango.md) but we need a more generic way to retrieve models and generate html template. Knowledge of Python and HTML is required.

### Add support of FODT for report ###
Tryton uses [Relatorio](http://relatorio.openhex.org/) has template engine. It uses [ODT](http://en.wikipedia.org/wiki/OpenDocument) file as template but the maintenance of zipped file in the [VCS](http://en.wikipedia.org/wiki/Revision_control) is complicated. The goal is to be able to use the FODT format as it is a flat-XML. Knowledge of Python and XML is required.

## Medium ##

### Add memcached support ###
[Memcached](http://www.danga.com/memcached/) is a high performance system for storing key/value pairs in memory. Memcached support could be added by allowing the server to create cache entries for data read by a client as well as invalidate entries when data is written by a client.  Such an implementation would improve performance for end users of the client. A good understanding of python and database transactions is required.

### Add historical time-line in the GTK client ###
The Tryton server has the capability to store versions of records as changes are made and to retrieve those past versions.  The Tryton client currently does not have the capability to access this information. To add the historical timeline a view would need to be created that allowed a user of the client to browse past versions of a record based on a date and time and optionally select an old version to write over the current version.  Knowledge of Python and PyGTK is required.

### Integrate Webshop Satchmo and Tryton ###
The goal will be to retrieve sales from [Satchmo](http://www.satchmoproject.com/) into Tryton and to update Satchmo products based on Tryton products. To achieve this goal module for Satchmo and for Tryton needs to be created that will allow communication between both applications. An asynchronous communication will be privileged. The system must stay as much possible modular to keep the spirit of both projects. Knowledge of Python is required.

### Implement a POS with Tryton ###
Tryton has the possibility to run as a standalone application using SQLite with the Neso module. The goals will be to be able to use it as a POS that can synchronize with a Tryton server. It will require to develop some specific widgets for POS (numeric pad, big button etc.) inside the GTK client. Knowledge of Python, PyGTK is required.

### Create a Python module to generate SQL strings ###
We would like to simplify the generation of SQL strings in Tryton (and generally in Python). The goals is to have a pythonic syntax for SQL, there is already a small example of desired syntax at [pysql](http://codereview.appspot.com/4248045/). Knowledge of Python and SQL is required.

### Port to Python 3 ###
Making Tryton working on Python 3 using the 2to3 script. Knowledge of Python is required.

### Implement Email Integration ###
Tryton has the goal to manage email. A [blueprint](EmailIntegration.md) exists about it. The goals is to provide an IMAP server based on twisted with Tryton as backend. Knowledge of Python is required and Twisted is better.

## Hard ##

### Add Gantt chart in the GTK client ###
The PyGTK client of Tryton already has [bar chart](http://en.wikipedia.org/wiki/Bar_chart), [line chart](http://en.wikipedia.org/wiki/Line_chart) and [pie chart](http://en.wikipedia.org/wiki/Pie_chart) using [Pycairo](http://cairographics.org/pycairo/). It will be great to have also [Gantt chart](http://en.wikipedia.org/wiki/Gantt_chart) to display project schedule. Such implementation would need to extend the xml definition of graph views. Optionally it could be great to make an external library with all the graphs rendering engine. Knowledge of Python, PyGTK and Pycairo is required. Knowledge of XML is optional.

### Add WYSIWYG text editor in the GTK client ###
The PyGTK client of Tryton has a simple text entry. It will be great to have a text entry that allow to format the text (alignment, font size, bullet etc.). Internal format could be a subset of html. Knowledge of Python, PyGTK is required. Knowledge of HTML is optional.

### Create a GWT client for Tryton ###
In some cases, it is better to have a web client than a thin one. So the goal is to write a client using the [GWT](http://code.google.com/webtoolkit/) that has the same functionality and design then the GTK client (for easy maintenance). As it is a long and hard job, it could be split into sub-projects. Knowledge of GWT is required. Knowledge of Python, pyGTK and JSON-RPC is optional.