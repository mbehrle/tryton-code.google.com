#summary Configuration and first start of Tryton
#labels Featured,Phase-Deploy

# Introduction #

# Install Tryton #
see the OS specific page.

# Setup a Database and User System #

```
$ sudo su postgres -c "createuser --createdb --no-adduser -P tryton"
$ sudo useradd tryton
```

# Start trytond #
```
$ cd ~/workspace/tryton-dist/trytond
$ sudo su tryton -c "bin/trytond"
```


# Configuration file #
The configuration file of the server is in _[etc/trytond.conf](http://hg.tryton.org/trytond/file/tip/etc/trytond.conf)_

# Start tryton #
```
$ cd ~/workspace/tryton-dist/tryton
$ ./bin/tryton
```

# Create a database #

  * Cancel login window

  * Click on File>Database>New Database

  * Fill the form and click on Create

  * Login with the user "admin"