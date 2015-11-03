# Introduction #

This page should provide infos about known problems when upgrading a version.


# Upgrade 2.8 -> 3.0 #

## Error message 'File not found: /usr/lib/python2.7/site-packages/trytond/modules/test/tryton.cfg ##

Due to a change, the 'test' scripts of the Tryton-Server have moved. When accessing the 'Modules' Section via the GUI, the a.m. error message appears. <br> Solution: Delete the entry from the database. Open a shell on the server (assuming you run a Linux-machine):<br>
<pre><code>sudo su postgres<br>
<br>
psql<br>
<br>
\c your_database_name<br>
<br>
delete from ir_module_module where name = 'test';<br>
<br>
\q<br>
</code></pre>