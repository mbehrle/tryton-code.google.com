# Introduction #
Tryton and modules its starting to be packaged on foresight linux. Foresight get the server and client.

You can check the packages on packages Listening http://www.rpath.org/web/repos/foresight/browse

# Details #

For the client:
```
sudo conary update tryton=@fl:2-devel
```
For the server:
```
sudo conary update trytond=@fl:2-devel
```

For install all-on-one:
```
sudo conary update group-tryton=@fl:2-devel
```


By Default foresight not comes with postgresql so you can run tryton using the sqlite3 configuration the file on /etc/tryton.conf

here a example:
```
#tryton.conf
[options]
db_type = sqlite
data_path = /home/zodman/
```

## Issues ##

For issues/problems related with foresight (because tryton have his own https://bugs.tryton.org/) you can submit one on http://issues.foresightlinux.org/browse/FL-2445