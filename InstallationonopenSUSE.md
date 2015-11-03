

# Introduction #

The current documentation describes the installation of Tryton server on an openSUSE 13.2 System

Many of the settings can be made from the GUI, but in case you dont have a GUI (e.g. on a server) it is described from a command-line view.

Check out /usr/share/doc/packages/trytond/tryton-server.README.SUSE for additional information.

# Basic Setup - Details #

## Install GNU Health with SUSE One-Click-Install ##

GNU Health is available as package for openSUSE. Unlike the installation with the bash-script as described in the GNU Health documentation, it follows the setup-guidelines of openSUSE and the Tryton Server as a set of additional modules.

The most easy way is probably to install GNU Health using the one-click-install, available for [all supported openSUSE and GNU Health Versions](https://software.opensuse.org/package/gnuhealth?search_term=gnuhealth).

You can now continue with the [Basic Setup of the Database](https://code.google.com/p/tryton/wiki/InstallationonopenSUSE#Basic_setup_of_database)


## Setting up the repositories for the Tryton server ##
Open a terminal window and log in as root ( _sudo su -_ )

Include the python-repository: <br>
<i>zypper ar -f <a href='http://download.opensuse.org/repositories/devel:/languages:/python/openSUSE_13.2'>http://download.opensuse.org/repositories/devel:/languages:/python/openSUSE_13.2</a> python</i>

Include the Tryton-Repository in the desired version - in this case Tryton 3.6: <br>
<i>zypper ar -f <a href='http://download.opensuse.org/repositories/Application:/ERP:/Tryton:/3.6/openSUSE_13.2'>http://download.opensuse.org/repositories/Application:/ERP:/Tryton:/3.6/openSUSE_13.2</a> tryton</i>

<h2>Install GNU Health</h2>

As an alternative approach to the one-click-install, you can install GNU Health manually.<br>
<br>
The following command installs it with all dependencies (Postgres-Database, Tryton-Server):<br>
<i><code>zypper install gnuhealth</code></i>

You can now continue with the <a href='https://code.google.com/p/tryton/wiki/InstallationonopenSUSE#Basic_setup_of_database'>Basic Setup of the Database</a>

<h2>Install the Tryton server</h2>

You may want to check for available modules using zypper. In case you feel that one or the other module is missing, feel free to contact the package maintainer.<br>
<br>
<i><code>zypper search trytond*</code></i> will list all available Tryton-Modules.<br>
<br>
To install Tryton with all available modules: <br>
<i><code>zypper install trytond*</code></i>

.....and delete those modules you dont need, e.g. <br>
<i>zypper remove trytond_account_be trytond_account_fr</i>

<h2>Install the Tryton Client</h2>

Tryton frontend for openSUSE is available from the same source as 'tryton'.<br>
<i><code>zypper install tryton</code></i>

<h2>Basic setup of database</h2>
Now all basic installations are made.<br>
<br>
As Tryton from release 3.4 onwards uses an encrypted password in the configuration, there are two options to set-up the database and Tryton:<br>
<ol><li>the database is created manually (recommended for productive environments)<br>
</li><li>the database shall be created from the Tryton client (recommended for test-server)</li></ol>

In general, lets configure the database authorisation first.<br>
<br>
<h3>Local authorisation</h3>

The postgres-database runs under the user <i>postgres</i> . In order to make changes to the database - create<br>
databases - we need to change the local authorisation.<br>
In <i>/var/lib/pgsql/data/pg_hba.conf</i>, change the line<br>
<br>
<pre><code>local   all             all                                     md5<br>
</code></pre>

to<br>
<br>
<pre><code>local   all             all                                     trust<br>
</code></pre>

Start the Service postgres (as root)<br>
<i>systemctl start postgresql</i>

Verify it has started correctly: <br>
<i>systemctl status postgresql</i>

You can now log in as user postgres ( <i>sudo su - postgres</i> ) to perform all below activities.<br>
<br>
<h3>Manual database creation</h3>

The Tryton Server runs under the user <i>tryton</i>, so we need to create him in the postgres DB:<br>
<br>
log-in as user postgres (su postgres) to maintain the password and authorisations for tryton: <br>
<i>psql -c "CREATE USER tryton WITH CREATEDB;"</i><br>

This should be sufficient as minimal settings for postgres. You can now create a database as user 'postgres':<br>

<i>psql -c "createdb mydb --encoding='UTF8' --owner=tryton;"</i>

Now you need to initialize the database for use with Tryton.<br>
Log in as user 'tryton' ( <i>sudo su - tryton -s /bin/bash</i> ) and run: <br>

<i>trytond -c /etc/tryton/trytond.conf -u res -d mydb</i>

<h3>Database creation from the Tryton-client</h3>

In order to create the database from the client, we need to enable the role 'tryton' for an encrypted password and need to store the password in the tryton configuration file.<br>
<br>
<i>Additional</i> to the above role creation we change the role 'tryton' for an encrypted pasword 'admin'<br>
<i>psql -c "ALTER ROLE tryton ENCRYPTED PASSWORD 'admin' ;"</i>

The password needs to be stored - encrypted - in the tryton config file (see <a href='https://code.google.com/p/tryton/wiki/InstallationonopenSUSE#Set_the_encrypted_password'>below</a> )<br>
<br>
<h2>Basic setup of Tryton Server</h2>

<h3>Mandatory entries</h3>
Now lets configure the settings for the Tryton server:<br>
Maintain the variables in /etc/trytond.conf, at least: <br>
<pre><code># type of database <br>
db_type = postgresql  <br>
# admin password for the Tryton server <br>
admin_passwd = admin<br>
</code></pre>

From <b>Tryton 3.4 onwards</b>, the configuration file has changed. It is now in <i>/etc/tryton/trytond.conf</i> .<br>
The required entries look like:<br>
<pre><code># The URI to connect to the SQL database (following RFC-3986)<br>
uri = postgresql://admin:DBAdminPassword@localhost:5432/<br>
<br>
# The path to the directory where the Tryton Server stores files.<br>
# The server must have write permissions to this directory.<br>
path = /var/lib/trytond<br>
</code></pre>

If your database resides on the same machine as the Tryton-Server, the URI entry may just be:<br>
<pre><code># The URI to connect to the SQL database (following RFC-3986)<br>
uri = postgresql:///<br>
</code></pre>

You may as well adapt the new log file configuration in <i>/etc/tryton/trytond_log.conf</i>

<h3>Set the encrypted password</h3>

From Tryton 3.4 onwards, the password is encrypted in the configuration file. To create the encrypted entry, run the command<br>
<pre><code>python -c 'import getpass,crypt,random,string; print crypt.crypt(getpass.getpass(), "".join(random.sample(string.ascii_letters + string.digits, 8)))'<br>
</code></pre>

For the password 'admin' you receive the key 'BF1ZdEC4NVcsM' which is entered in <i>/etc/tryton/trytond.conf</i> :<br>
<br>
<pre><code>[session]<br>
# Session settings<br>
super_pwd = BF1ZdEC4NVcsM<br>
</code></pre>

In case you have GNU Health installed, the script <i>/usr/share/doc/packages/gnuhealth/scripts/serverpass.py</i> would do the job.<br>
<br>
<h3>Start the Tryton Server</h3>

Now you can start the service tryton: <br>
<i>systemctl start trytond</i>

Check the status: <br>
<i>systemctl status trytond</i>

To enable tryton to start at startup: <br>
<i>systemctl enable trytond</i>

<h1>Advanced Server Configuration</h1>

In most cases you will not have server and client running on the same box, but use a distributed environment with<br>
<br>
<ul><li>using SSL for secure communication<br>
</li><li>server and client running on different machines<br>
</li><li>application server and database running on different machines</li></ul>

Some small adjustments are required to serve these scenarios.<br>
<h2>Setting up SSL communication with the Tryton server</h2>
Even if running only in the local network, the communication between the Tryton server and client should be secured using SSL. To enable the secured communication, a certificate is required. As long as Tryton is only used 'internal' (e.g. no external customers), a self-signed certificate is sufficient. If you have external partners accessing your system, they might get confused and a certificate from a CA authority might be the better choice.<br>
<br>
Next to various sources on the Internet, I found the description in<br>
<a href='https://mrnovell.wordpress.com/2009/06/18/opensuse-linux-creating-self-signed-ssl-certificates'>Mr. Novell's Blog</a> very useful to generate a self-signed cetificate.<br>
<br>
As long as you don't run a web-server on the same machine (which may be required to allow external customers access to your system via a frontend or a webshop), and put the certificats into the webserver's path, the question is where to store the self-signed certificates.<br>
<br>
As it is only for Tryton, I created a directory /etc/trytond and put the files into appropriate subdirectories (following the naming convention you find for apache as well, access only to root and group tryton):<br>
<br>
<pre><code>mkdir /etc/trytond<br>
mkdir /etc/trytond/ssl.key<br>
mkdir /etc/trytond/ssl.crt<br>
mkdir /etc/trytond/ssl.csr<br>
mv /path/to/certificates/server/tryton_server.key /etc/trytond/ssl.key/.<br>
mv /path/to/certificates/server/tryton_server.crt /etc/trytond/ssl.crt/.<br>
mv /path/to/certificates/server/tryton_server.csr /etc/trytond/ssl.csr/.<br>
chmod 0640 /etc/trytond*<br>
chmod +x /etc/trytond<br>
chown -R root:tryton /etc/trytond*<br>
</code></pre>

Now you need to maintain the settings in /etc/trytond.conf resp. /etc/tryton/trytond.conf:<br>
<pre><code>ssl_jsonrpc = True<br>
#Uncomment these lines if you use xmlrpc and webdav<br>
#ssl_xmlrpc = True<br>
#ssl_webdav = True<br>
privatekey = /etc/trytond/ssl.key/tryton_server.key<br>
certificate = /etc/trytond/ssl.crt/.tryton_server.crt<br>
</code></pre>

Restart the server:<br>
<i>systemctl restart trytond</i>

The client should automatically detect the SSL connection. In case you end up with an error like<br>
<pre><code>...<br>
File "/usr/lib/python2.7/httplib.py", line 371, in _read_status<br>
    raise BadStatusLine(line)<br>
BadStatusLine: ''<br>
</code></pre>
then there is a problem with your SSL setup, <b>or</b> the client has connected to the server before without using SSL. In the latter case, close the client and remove the file<br>
<pre><code>~/.config/tryton/x.y/known_hosts      # Fingerprints<br>
</code></pre>
from the user's home directory.<br>
<br>
<h2>Server and Client on different machines</h2>

First you need to enable the server to listen to clients from external.<br>
Change the variable in /etc/tryton.conf resp. /etc/tryton/trytond.conf: <br>
<pre><code>jsonrpc = *:8000<br>
</code></pre>
if the server should accept connections from any IP-address. Of course you can narrow to subnets to increase security.<br>
<br>
Next, its a good idea to set some parameters for the database connection, at least user and password (up to Tryton 3.2)<br>
<pre><code>db_user = tryton<br>
db_password = DBAdminPassword<br>
</code></pre>

For Tryton 3.4 and above you need to set an encrypted password, see <a href='https://code.google.com/p/tryton/wiki/InstallationonopenSUSE#Set_the_encrypted_password'>Set the encrypted password</a>

Finally you should check the configuration file of the database what kind of connections it allows. For PostgreSQL under openSUSE this is in  /var/lib/pgsql/data/pg_hba.conf . It should look similar to this:<br>
<pre><code># TYPE  DATABASE        USER            ADDRESS                 METHOD<br>
<br>
# "local" is for Unix domain socket connections only<br>
local   all             all                                     trust<br>
# IPv4 local connections:<br>
host    all             all             127.0.0.1/32            md5<br>
</code></pre>
Here the database accepts only connections from the same machine. This should be about it. Restart the server.<br>
<br>
<h2>Application Server and Database running on different machines</h2>

For larger installations a split between application server and database is recommended. For the Tryton server, you need to set the host and port parameters for the database. Postgres runs by default on port 5432:<br>
<pre><code>db_host = 192.168.2.100<br>
db_port = 5432<br>
</code></pre>

From <b>Tryton 3.4 onwards</b>, the configuration file has changed. It is now in <i>/etc/tryton/trytond.conf</i> .<br>
The required entries look like:<br>
<pre><code># The URI to connect to the SQL database (following RFC-3986)<br>
uri = postgresql://admin:DBAdminPassword@192.168.2.100:5432/<br>
</code></pre>


Additionally you need to tell the database where to accept connections from. In the a.m. pg_hba.conf file, set the subnet accordingly, for example:<br>
<pre><code># TYPE  DATABASE        USER            ADDRESS                 METHOD<br>
<br>
# "local" is for Unix domain socket connections only<br>
local   all             all                                     peer<br>
# IPv4 local connections:<br>
host    all             all             192.168.2.1/16            md5<br>
</code></pre>

Database and Server need a restart to apply the changes