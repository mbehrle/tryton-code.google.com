#summary Installation from DSCM Mercurial
#labels Phase-Deploy


# Introduction #

This page describes the installation process of Tryton from scratch.

If you don't manage to make development, we strongly suggest you to use the installation packages provided by your distribution. For installation hints for your preferred distribution please refer to the additional pages below:

  * InstallationWindows
  * InstallationFreeBSD
  * InstallationOnDebian
  * InstallationOnMandriva
  * InstallationOnFedora
  * InstallationOnForesightLinux
  * InstallationOnSlackware
  * GentooOverlay

[Mercurial](http://www.selenic.com/mercurial/wiki/index.cgi/Mercurial) is the distributed source control management system (DSCM) used by the Tryton project. The repository layout for the Tryton project is divided into
  * one repository for the client (tryton)
  * one repository for the server (trytond)
  * repositories for the modules, one for each module, prefixed by module/
  * the above structure copied for each release, prefixed by the release version
  * several other project related repositories

You need to install [Mercurial](http://www.selenic.com/mercurial/wiki/index.cgi/BinaryPackages) and [HgNested](http://code.google.com/p/hgnested/) ([Using Extensions](http://mercurial.selenic.com/wiki/UsingExtensions)) before you can follow this instructions.

# Installation #
The installation of Tryton is divided in four parts, following the three-tier architecture of Tryton
  1. Installation of [Requirements](Requirements.md)
  1. Client installation
  1. Server and modules installation
  1. Database installation
All of the three parts of Tryton can reside on different machines. The different tiers of Tryton are connected via a TCP/IP network.

## Client Installation ##

This section describes the installation process for `tryton` (the client application)

  * Creating a folder for tryton (the client) (we create the folder under ~/workspace)
```
mkdir ~/workspace/tryton-dist
cd ~/workspace/tryton-dist
```
  * Clone the hg repository
```
hg clone http://hg.tryton.org/tryton/
```

## Server and Modules Installation ##

This section describes the installation process for the trytond server application and the modules.

  * Creating a folder for trytond (the server) (we create the folder under ~/workspace)
```
mkdir ~/workspace/tryton-dist
cd ~/workspace/tryton-dist
```

  * Nested clone the hg repository
```
hg nclone http://hg.tryton.org/trytond
```

This will clone also all the modules in trytond/modules


## Updating Client, Server and Modules Repositories ##

  * The client
```
cd ~/workspace/tryton-dist/tryton
hg pull -u
```

  * The server and modules
```
cd ~/workspace/tryton-dist/trytond
hg npull -u
```


## Installing Tryton on your favourite distribution ##



## Database installation ##
trytond uses [PostgreSQL](http://www.postgresql.org/) as database engine.

The [PostgreSQL](http://www.postgresql.org/) database may be installed on the same machine as the trytond server application, but it can be on any machine connected via TCP/IP network.

Please refer to the appropriate [documentation](http://www.postgresql.org/docs/) for installing PostgreSQL on your operating system or distribution.