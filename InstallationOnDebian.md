

# Introduction #

This page contains some additional installation hints to [Installation from Mercurial](http://code.google.com/p/tryton/wiki/InstallationMercurial) for a Debian based system (as of 12/2013)

# Preliminary considerations #

It is important to take first the decision, if

  * **Option 1:** you want just run the latest release of Tryton (for testing, usage or production) on your Debian system

  * **Option 2:** you plan to develop with Tryton (therefore intending probably to run some versions in parallel resp. to run the trunk version (tip))

_Hint:_

_One time you have packages installed in the system, they will be in PYTHONPATH. This will result in conflicts, if you try to run any other version of Tryton different from the installed one. This problem also applies to dependencies being installed in parallel via easy\_install/pip **and** apt. Take care to use one or the other, but not both! On a Debian system the installation via apt is recommended, usually all needed dependencies are packaged for Debian._

# Option 1: Installation from package management #

Tryton packages are available since Debian Squeeze. As usual dependencies will be automatically resolved by the package management.

A synopsis of the available sources can be found at [Gitweb Tryton Packages](https://alioth.debian.org/plugins/scmgit/cgi-bin/gitweb.cgi?a=project_list&s=tryton%2F&btnS=Search)

Additionally to the official Debian packages backported packages are available for the different Tryton series. For more information have a look at

**http://tryton.alioth.debian.org**

and especially

**http://tryton.alioth.debian.org/mirror.html**

_Hint:_

_If you want to install all available Tryton modules at once, search for package tryton-modules-all._

After installation have a look at /usr/share/doc/tryton-server/README.Debian for the installed version of tryton-server (**[click here to see the latest version of README.Debian in the VCS](https://alioth.debian.org/plugins/scmgit/cgi-bin/gitweb.cgi?p=tryton/tryton-server.git;a=blob_plain;f=debian/tryton-server.README.Debian;hb=HEAD)**).

Complete the configuration of your system and you are done (**[click here to see the latest version of a commented version of trytond.conf in the VCS](https://alioth.debian.org/plugins/scmgit/cgi-bin/gitweb.cgi?p=tryton/tryton-server.git;a=blob;f=debian/trytond.conf;h=fd28e1f6d398694b36535284b4797338c43fdce5;hb=HEAD)**).


# Option 2: Running from sources or in a virtual Python environment #

## Running from sources ##

### Installation of dependencies ###

Generally all dependencies for Tryton are packaged for Debian and can be installed with the package management.

Take a look at the dependencies of the **[client](https://alioth.debian.org/plugins/scmgit/cgi-bin/gitweb.cgi?p=tryton/tryton-client.git;a=blob;f=debian/control;hb=HEAD)** and of the **[server](https://alioth.debian.org/plugins/scmgit/cgi-bin/gitweb.cgi?p=tryton/tryton-server.git;a=blob;f=debian/control;hb=HEAD)**, that can easily be installed with 'apt-get install _package\_name_'

_Note:_

_Optional dependencies are listed under Recommends._

_Modules can require additional dependencies._

### Get the sources ###

```
$ sudo apt-get install mercurial mercurial-nested
```

if you want to use the hgnested extension (recommended) [HgNested](http://code.google.com/p/hgnested/) ([Using Extensions](http://mercurial.selenic.com/wiki/UsingExtensions)) you can enable it for the user the following way:

Take a look at /etc/mercurial/hgrc.d/hgnested.rc, how to activate the extension or just do

```
$ echo -e "[extensions]\nhgnested=" >> ~/.hgrc
```


### Download ###

Just proceed as described in [Installation](http://code.google.com/p/tryton/wiki/InstallationMercurial#Installation).

When downloading and running from sources, **_do NOT_ install those packages with setup.py!** Just run the binaries from the sources.


## Running in a virtual environment ##

  * It is higly recommended to run pip on Debian systems in a virtual environment. You have been warned.

In short:

```
$ sudo apt-get install python-virtualenv virtualenvwrapper
```

  * The usage of virtualenv is out of the scope of this document, please refer to the documentation of python-virtualenv