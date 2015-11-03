

# Installing the Client #

The **best** way for installing the Tryton client on Mac OS X is: download the client from the [download page](http://www.tryton.org/download.html). There you find a self-contained package and nothing to worry about.

# Installing the Server #

Currently we do not provide packages for the server. Sorry!

Installation via MacPorts relatively straight forward, however.

  1. Download and install [MacPorts](http://www.macports.org/install.php)
  1. Install PostgreSQL
```
sudo port install postgresql84 postgresql84-server
```
  1. Install python
```
sudo port install python26 py26-setuptools
```
  1. Using easy\_install, install trytond
```
sudo /opt/local/bin/easy_install-2.6 trytond
```
  1. Optionally install some modules, like so:  (A full list can be found [here](http://pypi.python.org/pypi?%3Aaction=search&term=trytond_&submit=search))
```
sudo /opt/local/bin/easy_install-2.6 trytond_product
```
  1. Start the server
```
sudo /opt/local/Library/Frameworks/Python.framework/Versions/2.6/bin/trytond
```