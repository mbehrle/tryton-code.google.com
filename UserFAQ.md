#summary Frequently ask Questions for using Tryton
#labels Phase-Support


## Tryton Client ##
### Can I use Tryton on KDE/Qt? ###
Yes, Tryton works fine inside KDE and Qt. The Tryton Client does not make use of KDE/QT widgets.

### Problems to identify focussed buttons or other graphical elements ###
If you have problems with highlighting focussed widgets in KDE, so that you can't identify visually where the input cursor is, this may depend on using the [GTK-Qt Theme Engine](http://gtk-qt.ecs.soton.ac.uk/index.php). In case you have such problems you can try to edit the System Settings of KDE. Just open the 'Look and Feel' > Appearance panel and set the GTK Styles to "Raleigh" or try out something different then "Use my KDE style in GTK applications".

### How to change the language? ###
  1. To show all translations of Tryton, go to `Menu: Administration > Localization > Languages` and check the _Translatable_ field of your preferred languages.
  1. After this you need to update all installed modules in the database. Stop a running Tryton Server (trytond) and start the trytond database update with `sudo su TRYTONUSER -c "PATH/TO/bin/trytond -u all -d DATABASENAME"`. (Change TRYTONUSER, PATH/TO/ and DATABASENAME to your computer systems need.) When done, restart tytond as you usual do.
  1. To choose another languages for your users, open `Menu: Administration > Users > Users`. Select in the _Preferences_ tab the _Language_ your users prefer.

The new localisation apply with the next log in of a user.

### But some elements are not translated ###
First find out if your language is already supported by Tryton. If your language is supported by Tryton it is still possible, that some standard GTK elements like the "Ok" or "Cancel" button are not correctly translated. To solve this issue you need to install the system language package for GTK:  language-pack-gnome-de-base (Ubuntu) or libgtk2.0-common (Debian).

### Can I set my own shortcuts in the menu? ###
Yes, it is possible. Just go to Options/Menubar/Change Accelerators to enable the setting of own shortcuts in the GTK-specific way:
Focus first the menu item via mouse or keyboard and press then the desired key (combination).

After setting your desired shortcuts, it is perhaps best to disable the feature again to avoid changes by accident.

### I'm getting "Incompatible version of the server" ###
The Tryton client (tryton) and server (trytond) you're trying to connect to must have the same [major version](ReleaseGeneral#Version_number_of_Tryton_releases.md).
  1. Check the version of the client: `tryton --version`
  1. On the machine running trytond, check the version of the server: `trytond --version`
  1. Fix your installation.

### I'm getting "Could not connect to server" ###
  1. Check if the server is running: `ps aux | grep trytond`
  1. Check the address and port the server is accepting connections to: `netstat -tupan | grep python`
  1. If necessary fix your [server configuration](SetupAndStart#Configuration_file.md).
  1. Check if any networking issue (firewall, routing etc.) is preventing you from connecting to the server: `telnet server_host server_port`
  1. Currently Tryton misleadingly reports database connection problems as "Could not connect to server" ([issue2842](https://bugs.tryton.org/issue2842)):
    * Check if the database server is running: `ps aux | grep postgres`
    * Check if you can authenticate to the database server: `sudo -u system_user psql -h db_host template1 db_user` where `system_user` is the system user the Tryton daemon is running under and `db_host` and `db_user` is the database host and user respectively from your trytond.conf. If necessary fix your trytond.conf or the [client authentication of PostgreSQL](http://wiki.postgresql.org/wiki/Client_Authentication).
    * Check if psycopg2 is installed.

### I have installed a module with easy\_install, pip or a package manager, but it doesn't show up in the list under Administration > Modules > Modules. ###
You have to upgrade one module of the corresponding database, if you're unsure what module to update, you can run `trytond -d db_name -u all` ([issue2638](https://bugs.tryton.org/issue2638)).