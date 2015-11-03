[![](http://code.google.com/images/GSoC2012_300x200.png)](http://code.google.com/soc/)


# Ideas #

Post your ideas for students during [Google's Summer of Code 2012](http://code.google.com/soc/) here. See the [FAQ entry](https://google-melange.appspot.com/document/show/gsoc_program/google/gsoc2012/faqs#ideas_list) on the ideas list for further details.

## Easy ##

### Add support of FODT for report ###
Tryton uses [Relatorio](http://relatorio.openhex.org/) has template engine. It uses [ODT](http://en.wikipedia.org/wiki/OpenDocument) file as template but the maintenance of zipped file in the [VCS](http://en.wikipedia.org/wiki/Revision_control) is complicated. The goal is to be able to use the FODT format as it is a flat-XML. Knowledge of Python and XML is required.

### Historize attachments ###
Create a module that historizes attachments and exposes versions/revisions via the WebDAV protocol. Knowledge of Python and HTTP is required.

### Complete demo script ###
Tryton runs a demo server where people can test the software. To give to the people a great experience, it is good that the software is filled with credible data with an historic. So we have a script [tryton\_demo.py](http://hg.tryton.org/tryton-tools/file/3a30c988c7ff/tryton_demo.py) that is far to be complete. So the goals is to complete it by keeping its modular approach. Knowledge of Python and business software is required (it is better to also know the TV show [The Office](https://en.wikipedia.org/wiki/The_Office_%28U.S._TV_series%29) as the data are based on this virtual company).

### Website on top of PyPI ###
The goal is to provide a website to promote Tryton modules and implement a trust network of scoring. The website must take information from [PyPI](http://pypi.python.org/pypi). Knowledge of Python, HTML is required.

## Medium ##

### Python-SQL ###
Complete the current implementation of pyton-sql, a python library to generate SQL statement in a pythonic way. (see https://code.google.com/p/python-sql/)
The goal is to replace manual SQL string generation by python-sql. Knowledge of Python and SQL is required.

### Add historical time-line in the GTK client ###
The Tryton server has the capability to store versions of records as changes are made and to retrieve those past versions. The Tryton client currently does not have the capability to access this information. To add the historical timeline a view would need to be created that allowed a user of the client to browse past versions of a record based on a date and time and optionally select an old version to write over the current version. Knowledge of Python and PyGTK is required.

### Add generic comments to the GTK client ###
Just like Tryton can have attachments to any records, it will be great to have the same for comments. The widget should show the history of all comments and prevent user to edit old comments. Knowledge  of Python and PyGTK is required.

### Add a calendar view ###
Using GooCalendar, it will be great to display some records inside a calendar view.
The view should take care of fetching only the displayed records base on a date or a couple of dates. It should be possible to add, remove or edit any event with the form view. Knowledge of Python, PyGTK and GooCanvas is required.

## Hard ##

### Add Gantt chart in the GTK client ###
The PyGTK client of Tryton already has [bar chart](http://en.wikipedia.org/wiki/Bar_chart), [line chart](http://en.wikipedia.org/wiki/Line_chart) and [pie chart](http://en.wikipedia.org/wiki/Pie_chart) using [Pycairo](http://cairographics.org/pycairo/). It will be great to have also [Gantt chart](http://en.wikipedia.org/wiki/Gantt_chart) to display project schedule. Such implementation would need to extend the xml definition of graph views. Optionally it could be great to make an external library with all the graphs rendering engine. Knowledge of Python, PyGTK and Pycairo is required. Knowledge of XML is optional.