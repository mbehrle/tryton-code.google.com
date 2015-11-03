#summary How to install Tryton server on FreeBSD
#labels Phase-Deploy


# Installing the Client #

Currently the Tryton client is not part of the FreeBSD [ports collection](http://www.freshports.org).

# Installing the Server #

The server **trytond** is part of the FreeBSD [ports collection](http://www.freshports.org). Installing it via ports will give you the advantage of resolving and installing all dependencies, but leaves you without tryton modules (and their dependencies). To get full advantage of Tryton several extra steps are recommended:

## Database ##

### PostreSQL Server ###

[PostgreSQL](http://www.postgresql.org/) database may run on the same or another machine. Installation for FreeBSD is described [here](http://screamingelectron.org/forum/showthread.php?t=2992).

### PostreSQL Client ###

Install the PostgreSQL client version corresponding to your server via ports collection _before_ installing **trytond**.

### SQLite ###

[SQLite](http://www.sqlite.org/) support is new since version 1.4 of tryton and can be installed equivalent.

## trytond ##

**portupgrade** will come in handy, so make sure it is installed.
```
cd /usr/ports/ports-mgmt/portupgrade
make install
rehash
```
  1. Install trytond via ports collection to get all dependencies installed.
```
portinstall trytond
```
  1. deinstall trytond and Python Openssl package.
```
pkg_deinstall trytond
pkg_deinstall py26-openssl
```
  1. Install mercurial
```
portinstall mercurial
```
  1. Create a workspace with directories for the branches you want. for example 1.4 and development branch.
```
mkdir -p ~/workspace/tryton/dev/disabled_modules
mkdir -p ~/workspace/tryton/1.4/disabled_modules
```
  1. Get [tryton-dev.py](http://hg.tryton.org/hgwebdir.cgi/tryton-dev/raw-file/tip/tryton-dev.py) script, save it to your workspace and make it executable.
```
chmod +x ~/workspace/tryton-dev.py
```
  1. Fetch the development branch.
```
cd ~/workspace/tryton/dev
~/workspace/tryton-get.py
```
  1. Install some python dependencies and extra functionality.
```
easy_install BeautifulSoup
easy_install vobject
easy_install pyWebDav
easy_install -U pyWebDav
easy_install pyOpenSSL
easy_install vatnumber
portinstall py26-soappy
```
> Since i did not manage to install python ldap i moved these modules away for now ([help welcome](mailto:ok@monkeytower.net)).
```
mv trytond/trytond/modules/*ldap* disabled_modules
```
  1. repeat the last steps for 1.4 branch
```
cd ~/workspace/tryton/1.4
~/workspace/tryton-get --branch 1.4
easy_install BeautifulSoup
easy_install vobject
easy_install pyWebDav
easy_install -U pyWebDav
easy_install pyOpenSSL
easy_install vatnumber
portinstall py26-soappy
mv trytond/trytond/modules/*ldap* disabled_modules
```
# Initial configuration and server start #
  1. Copy the configuration file to /usr/local/etc
```
cp ~workspace/tryton/dev/trytond/etc/trytond.conf /usr/local/etc/trytond/trytond.conf
```
  1. These options are important:
```
db_type = postgresql
db_user = trytondbuser 
admin_passwd = secretadminpassword
```
  1. Start the server
```
~/workspace/tryton/dev/trytond/bin/trytond
```