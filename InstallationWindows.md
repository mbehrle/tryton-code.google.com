#summary How to install Tryton Client and server on Windows
#labels Phase-Deploy


# Installing the Client #

The **best** way for installing the Tryton client on Window$ is: download the client from the [download page](http://downloads.tryton.org). There you find a self-contained package and nothing to worry about.

# Installing the Server #

<sup>(works for Win$ 7 and tryton 3.4)</sup>

## Download required packages ##

  * Create a folder for the downloaded sources. Ex: C:\TrytDwn
  * <a href='http://www.postgresql.org/download/windows/'>Download PostgreSQL</a> <a href='http://www.enterprisedb.com/products-services-training/pgdownload#windows'>(mirror)</a>
  * <a href='https://www.python.org/downloads/'>Download Python</a>
  * <a href='http://www.pygtk.org/downloads.html'>Download PyGTK (all-in-one msi)</a>
  * <a href='http://labix.org/python-dateutil'>Download python-dateutil</a> <a href='https://pypi.python.org/pypi/python-dateutil/'>(from PyPI)</a>
  * <a href='https://pypi.python.org/pypi/python-sql/'>Download python-sql</a>
  * <a href='https://pypi.python.org/pypi/simplejson'>Download simplejson</a>
  * <a href='http://www.bytereef.org/mpdecimal/download.html'>Download cdecimal</a>
  * <a href='https://pypi.python.org/pypi/pycparser'>Download Pycparser</a>
  * <a href='https://pypi.python.org/pypi/bcrypt'>Download bcrypt</a>
  * <a href='https://pypi.python.org/pypi/cffi'>Download cffi</a>
  * <a href='http://www.stickpeople.com/projects/python/win-psycopg/'>Download psycopg 2</a>
  * <a href='https://pypi.python.org/pypi/GooCalendar'>Download GooCalendar</a>
  * <a href='https://pypi.python.org/pypi/lxml/3.4.2#downloads'>Download lxml</a>
  * <a href='https://pypi.python.org/pypi/relatorio'>Download relatorio</a>
  * <a href='https://pypi.python.org/pypi/polib/'>Download polib</a>
  * <a href='https://pypi.python.org/pypi/fcrypt'>Download fcrypt</a> <a href='https://stackoverflow.com/a/21106284'> (why fcrypt?)</a>
  * <a href='https://www.libreoffice.org/download/libreoffice-fresh/'>Download LibreOffice</a> (for the UNO libraries)
  * <a href='http://download.microsoft.com/download/A/5/4/A54BADB6-9C3F-478D-8657-93B3FC9FE62D/vcsetup.exe'>Download Visual Studio C++</a> (for msvcr90.dll) <a href='https://stackoverflow.com/a/18045219'> (source)</a>
  * <a href='http://downloads.tryton.org/3.4/trytond-3.4.2.tar.gz'>Download tryton server</a> (trytond)
  * <a href='http://downloads.tryton.org/3.4/tryton-setup-last.exe'>Download tryton client</a> (tryton)
  * <a href='http://www.7-zip.org'>Download 7-zip</a> (or equivalent)

## Change the clock to UTC ##

(<a href='http://comments.gmane.org/gmane.comp.python.tryton.devel/7604'>source 1</a>; <a href='http://crashmag.net/configuring-windows-7-support-for-utc-bios-time'>source 2</a>)
  1. Start the Registry Editor (run regedit from start menu)
  1. Look for the following path: HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation
  1. Create a dword named RealTimeIsUniversal and set the value to 1
  1. Restart your computer
  1. Open time and date settings
  1. Change to UTC

## Install PostgreSQL ##

  * Double-click on the MSI or EXE file of PostgreSQL
  * Select the following optiions
    * pgAgent
    * pgBouncer
    * Apache/PHP
    * phpPgAdmin
  * Make sure to set and remember a safe password
  * Allow strange characters by adding the following line in postgresql.conf (<a href='http://permalink.gmane.org/gmane.comp.python.tryton.spanish/2717'>source</a>; optional?):
`bytea_output == 'escape'`
  * Restart the server
    * Go to Start Menu --> PostgreSQL --> Reload configuration

## Install 7-zip (or equivalent) and LibreOffice ##

This guide was prepared using LibreOffice 4.3
Double click the EXE or MSI files

## Install Python ##

  * Install Python (double click EXE or MSI files)
  * Add a variable called PythonPath to the environment
    * META KEY + PAUSE --> Advanced system configuration --> Environment variables --> New
    * Set the value to  C:\Python27;C:\Python27\Lib\site-packages;C:\Python27\Scripts;C:\Python27\DLLs
    * (restart?)

## Decompress tar.gz and zip files ##

(It is convenient to decompress to the same directory)
  1. Go to the download folder
  1. select all the tar.gz files
  1. Right click on the files
  1. 7-zip --> Extract here
    * If a `dist` directory is created, open it.
    1. Select all tar files
    1. Right click on the files
    1. 7-zip --> Extract here
  * You should end up with a list of folders with the names of the packages to install
  1. Go to the download folder again
  1. Right click on the zip files
  1. Extract files to `dist` directory

## Start a Window$ console as administrator ##

Start menu --> Accesories --> Right click on System console --> Run as administrator

## Make sure to have vcvarsall.bat ##

(<a href='https://stackoverflow.com/a/18045219'>source</a>)
<br>
Install Visual Studio C++ to fix error: Unable to find vcvarsall.bat<br>
<br>
<b>SQL express is not necessary</b>

<h2>Install packages</h2>

For each package, go to their directory (Ex: <code>cd C:\TrytDwn\dist\&lt;package&gt;</code>) and install by typing (<code>python setup.py install</code>, unless otherwise noted)<br>
<ul><li>python-dateutil<br>
</li><li>python-sql<br>
</li><li>simplejson<br>
</li><li>cdecimal<br>
</li><li>Pycparser<br>
</li><li>bcrypt<br>
</li><li>cffi<br>
</li><li>psycopg 2 <b>with the win32 EXE</b>
</li><li>GooCalendar<br>
</li><li>lxml <b>with <code>pip install lxml</code></b> in the console<br>
</li><li>relatorio<br>
</li><li>polib<br>
</li><li>tryton server (trytond)<br>
</li><li>(tryton) <b>with the EXE</b> (tryton-setup-last.exe)</li></ul>


<h2>Create a tryton user in PostgreSQL</h2>

Open the PostgreSQL server on pgAdmin III<br>
<ul><li>Start menu --> PostgreSQL --> pgAdmin III --> Double click on the PostgreSQL server (below Servers) --> Type password --> Create a role for tryton<br>
</li><li>Right click on Login Roles --> New login role<br>
<ul><li>Set role for your tryton database user<br>
<ul><li>Set role name<br>
</li><li>Set and remember a safe password for the <tryton database user><br>
<ul><li>Role Privileges<br>
<ul><li>Can login<br>
</li><li>Inherits rights<br>
</li><li>NO superuser<br>
</li><li>Can create databases<br>
</li><li>NO create roles<br>
</li><li>NO initiate streaming replication and backups</li></ul></li></ul></li></ul></li></ul></li></ul>

<h2>Create a test database</h2>

<ul><li>Open the PostgreSQL server on pgAdmin III<br>
</li><li>Create a new database for which tryton is the owner<br>
<ul><li>Right click on Database --> New Database --><br>
<ul><li>Set the name of the database<br>
</li><li>Pick your <tryton database user> as owner<br>
After creating the user and database, you can close pgAdmin III</li></ul></li></ul></li></ul>

<h2>Create trytond.conf</h2>

<ul><li>Get the encrypted version of the <tryton database user> password:<br>
<ul><li>Run the following command in a console:<br>
</li></ul><blockquote><code>python -c 'import getpass,fcrypt,random,string; print fcrypt.crypt(getpass.getpass(), "".join(random.sample(string.ascii_letters + string.digits, 8)))'</code>
</blockquote><ul><li>Copy the resulting code</li></ul></li></ul>

<ul><li>Open a notepad window<br>
</li><li>Paste the following (replace passwords):<br>
<pre><code>[jsonrpc]<br>
listen == localhost:8000<br>
hostname == localhost<br>
<br>
[database]<br>
uri == postgresql://tryton:&lt;tryton password in pgAdmin&gt;@localhost:5432/<br>
<br>
[session]<br>
timeout == 600<br>
super_pwd == &lt;&lt; CTRL + V (to paste the resulting code of password) &gt;&gt;<br>
<br>
[report]<br>
unoconv == "C:\Program Files\LibreOffice 4\program\python.exe" unoconv<br>
</code></pre></li></ul>

<ul><li>Save as trytond.conf in a directory (preferably the c:\python27\scripts)</li></ul>

<h2>Install LibreOffice</h2>

Double click on the MSI installer (check that the installation directory is the same as the one in the line of unoconv in trytond.conf)<br>
<br>
<h2>Initialise database</h2>

(<a href='http://doc.tryton.org/3.4/trytond/doc/topics/setup_database.html'>source</a>)<br>
Type the following in a console:<br>
<blockquote><code>python &lt;path to Python scripts&gt; -c &lt;path to trytond.conf&gt; -d &lt;name of database&gt; --all</code>
<blockquote>Ex: <code>pytyon c:\Python27\Scripts\trytond -c c:\Python27\Scripts\trytond.conf -d test --all</code>
Set and remember a password for the admin user of the database (it can be different than the password of the tryton user set before)</blockquote></blockquote>

<h2>Run tryton server (trytond)</h2>

Type the following in a console:<br>
<blockquote><code>pytyon &lt;path to Python scripts&gt; -c &lt;path to trytond.conf&gt;</code>
<blockquote>Ex: <code>pytyon c:\Python27\Scripts\trytond -c c:\Python27\Scripts\trytond.conf</code>}</blockquote></blockquote>

<h2>Run tryton client (tryton)</h2>

In the openning window, set the server to localhost:8000 (that is, server localhost and port 8000), the user to admin and password to the one used when the database was initialised.