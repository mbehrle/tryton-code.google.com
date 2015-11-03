# Introduction #

This page contains some additional installation hints for installing on a Fedora or Redhat based system.

For installing the packages, simply open a console window with administration rights (a so called "root console") and paste the lines below into the console.

`yum` is the command-line version of the software installation center. Pasting  the lines into a window is much easier than selecting the packages via the GUI :-) plus for the server you need additional Python packages which are not available via the software installation center.

# For the Client #

... to be written ...

# For the Server #

  * Fedora 10:
```
yum install python-psycopg2 mx python-lxml python-genshi PyYAML
# needed for installing additional modules from PyPI
yum install python-setuptools-devel
yum install python-relatorio
easy_install -U pycha # may take a while (NB: pycha, not PyChart)

# optional dependencies
yum install pyOpenSSL
yum install pydot pytz python-BeautifulSoup python-vobject
urpmi openoffice.org-writer-core openoffice.org-pyuno
easy_install -U pywebdav openoffice-python vatnumber
```

  * CentOS 6.4:
```
yum install python-psycopg2 mx python-lxml python-genshi PyYAML
yum install python-setuptools-devel
yum install python-relatorio
yum install python-pip
yum install pyOpenSSL
yum install pyOpenSSL
yum install pydot pytz python-vobject urpmi openoffice.org-writer-core openoffice.org-pyuno
yum install gcc python-devel
yum install python-ldap
yum install crypto-utils
```

# Database installation #

  * Fedora 10
```
yum install postgresql-server
```

  * CentOS 6.4

On CentOS is older PostgreSQL database. You could install a newer vesion on http://yum.postgresql.org/

```
wget http://yum.postgresql.org/9.2/redhat/rhel-6-i386/pgdg-centos92-9.2-6.noarch.rpm
rpm -ivh pgdg-centos92-9.2-6.noarch.rpm
```

Install PostgreSQL

```
yum install postgresql92-server
```

Start Postgres and finish configuration:

```
service postgresql-9.2 initdb
service postgresql-9.2 start
chkconfig postgresql-9.2 on #start postgres when restart server
```

Configure pasword connections on localhost edit /var/lib/pgsql/9.2/data/pg\_hba.conf and change pear to md5.

```
# "local" is for Unix domain socket connections only
local   all             all                                     md5
```

And restart when finish all changes:

```
service postgresql-9.2 restart
```

Finally, create a new user and new ROLE to createdb

```
createuser --pwprompt userdb
ALTER ROLE userdb WITH CREATEDB;
```

Please refer to the appropriate [documentation](http://www.postgresql.org/docs/) for more information about how to set up PostgreSQL once you installed the package.

# Mercurial installation #

  * CentOS 6.4
On CentOS, Mercurial version is older. You could install a newer vesion:

```
wget http://pkgs.repoforge.org/mercurial/mercurial-2.2.2-1.el6.rfx.x86_64.rpm
yum install mercurial-2.2.2-1.el6.rfx.x86_64.rpm
```