

# Install from repository #

## Tryton client ##
Tryton can be installed from official Ubuntu repository. Just search in Ubuntu software center with pattern **tryton-client** and click install. Another way is open a terminal and type:
```
sudo apt-get install tryton-client
```

## Tryton server ##
Installation of Tryton server is the same as client. Appropriate package name is **tryton-server**. All modules can be installed with meta-package **tryton-modules-all**:
```
sudo apt-get install tryton-server tryton-modules-all
```

# Install from PPA #
Version of Tryton in official Ubuntu repository can be outdated. If you need the latest version you can use these PPAs:
  * [Tryton 2.6 series](https://launchpad.net/~rayanayar/+archive/tryton-2.6)
  * [Tryton 2.8 series](https://launchpad.net/~rayanayar/+archive/tryton-2.8)
  * [Tryton 3.0 series](https://launchpad.net/~rayanayar/+archive/tryton-3.0)
  * [Tryton 3.2 series](https://launchpad.net/~rayanayar/+archive/tryton-3.2)
  * [Tryton 3.4 series](https://launchpad.net/~rayanayar/+archive/tryton-3.4)
  * [Tryton 3.6 series](https://launchpad.net/~rayanayar/+archive/tryton-3.6)

PPA can be [activated in Software sources](https://help.ubuntu.com/community/Repositories/Ubuntu#Adding_PPAs) or by command:
```
sudo add-apt-repository ppa:rayanayar/tryton-3.6
sudo apt-get update
```

After activating the PPA, you can install desired packages by the same way as install from repository.

# Configuration #

The configuration of Tryton on Ubuntu is the same as on Debian, so please generally refer to [Installation on Debian](http://code.google.com/p/tryton/wiki/InstallationOnDebian) and especially have a look at **/usr/share/doc/tryton-server/README.Debian** to complete the configuration of your system.