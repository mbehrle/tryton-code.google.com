

There are many possibilities to connect Tryton with LDAP services like login process, general party attributes or the Tryton Access Groups.
This document collect the planning and discussions about the details of connecting Tryton to LDAP.
Since there are a number of potential sub-modules that could use LDAP resources, we should first have an LDAP base module.
One of the goals of every submodule should be to get information from ldap every time, rather than sync information with ldap.
Why? User "Joe" gets added to ldap, his email is "joe@example.com".
His email is changed in ldap to "Joe@asdf.com" when he moves to a new isp, but with syncing on demand the data already exists so Joe's info never gets update in Tryton, and messages sent to him through Tryton now don't reach him. However, if Joe is never actually in Tryton, then every request for his info goes over to the LDAP server and it is always accurate as per LDAP.

# LDAP connection module (done) #
The LDAP connection module should be used to define LDAP resources that can be used by other modules, rather than having each module define this stuff itself. An ldap resource should be defined as a single LDAP server.

  * Administration -> LDAP
  * Administration -> LDAP -> Connection
    * Form View with the fields:
      * Server fields.Char
      * Port fields.Int (auto filled in to 389 or 639 depending on ssl)
      * Secure fields.Selection (Never, SSL, TLS).
      * Bind DN fields.Char (empty for anonymous)
      * Bind Pass fields.Char, widget="sha"
      * Active Directory fields.Boolean
      * a button "Test Connection"

# LDAP connection Sources (done) #
Tryton module: [ldap\_connection](http://hg.tryton.org/hgwebdir.cgi/modules/ldap_connection/)

# LDAP Authentication (done) #
We started to integrate the TinyERP LDAP Module from Cédric Krier to Tryton. But in developing there came some major design issues of the old module we like to discuss:
  * Where to store LDAP connection details? We have reached the conclusion that the correct place for the connection.
The module will also need to override users
    * There is currently some replication of data because tryton settings are stored in tryton, not in ldap. Therefore a tryton user exists for every ldap user that logs in. This means that when an ldap user is removed, the tryton user must also be removed. Perhaps we could avoid replcation by overriding the user object to return ldap results aswell as tryton db results. It would be best, of possible, to avoid storing any information in tryton to avoid potential replication and errors caused by this.
  * How should Tryton handle local users? I believe the way to do this is to do what nss does. If a user is in ldap, that user info is used. If a user is not in ldap but is on the local system, that user info is used. If neither, user is not authed. Auth should fail closed, so if ldap can't be reached and the user doesn't have a local password, the user is denied access. Passwords should not be stored in both systems, only in ldap.

## LDAP Authentication Sources and Links (done) ##
Tryton module: [ldap\_authentication](http://hg.tryton.org/hgwebdir.cgi/modules/ldap_authentication/)

Original TinyERP Module from Cedric Krier: [users\_ldap](http://bazaar.launchpad.net/~activity/openobject-addons/trunk-extra-addons/files/3344?file_id=svn2bzr-ee7137a996279ce5318aa8c14112c06bc30e1872)

# LDAP Server #
The goal is to provide an LDAP server using Tryton as backend.

It could be based on [ldaptor](http://webmail.inoi.fi/open/trac/ldaptor) based on [Twisted](http://twistedmatrix.com/trac/).
An other way could be [pyasn1](http://pyasn1.sourceforge.net/) which contains a LDAP asn.

Modules could be writen to add Models to the LDAP tree.

# LDAP Party #
This integration is a synchronised mapping between people and organizations in Tryton and LDAP. So all this informations can be used system wide.

## Direct mapping database tables to LDAP ##
Since the synchronisation of Tryton data and LDAP data is hard to maintain, never up-to-date and not aware of changes in the affected module structure there could be other ways to go.

One other way to get the Tryton data into LDAP, is to provide an own LDAP service with the Tryton database as backend. Tryton aims to be a single point of data entry for business and additionally it try to serve these data in some common ways. So why not be a backend for a LDAP Server? With this there are no more synchronisation problems between Tryton and LDAP, because both realy use the same data.
LDAP can be infinitely replicated, so it would be possible just to set up an ldap mirror on the same box as tryton and then use local sockets to connect.

I haven't found any module which emulates an open LDAP server in Python. But there are other possible solutions: using an own deployment of LDAP with postgres as a database backend. (I don't believe this is really the way to do things. LDAP is a directory, it has it's own db engine. It's very possible to do this, but I feel it's desireable. Such a solution increases the complexity of the ldap configuration and pushes our problem off on to the user. Perhaps there should be more discussion on this.

It seems it would be possible to override the ORM so that queries sent to ldap are processed from a different data source. Though this seems like it could be a lot of work, I believe it would be the right way to do things. If our implimentation was well documented it could make future implimentations of similar things easier. There are many potential data sources, and often they cannot be changed to work with Tryton. Tryton should be able to work with them.


## LDAP Party Sources and Links ##
TinyERP module from Camptocamp: [c2c\_contact\_to\_ldap](http://bazaar.launchpad.net/~openerp-commiter/openobject-addons/4.2-extra-addons/files/115?file_id=c2c_contact_to_ldap-20080715131540-8ful0kum424x5n3g-3)

[ldap\_pg](http://www.samse.fr/GPL/ldap_pg/HOWTO/index.html)

# LDAP Access #
This integration controls the Tryton access rights from LDAP definitions. (This should be ldap groups, perhaps linked to ldap auth. I'd suggest this be the next project)


# General LDAP Sources and Links #
General informations about LDAP (Lightweight Directory Access Protocol):
http://en.wikipedia.org/wiki/Ldap

LDAP in Python: [python-ldap](http://python-ldap.sourceforge.net/doc/html/ldap.html)

[Python LDAP Applications](http://www.packtpub.com/article/installing-and-configuring-the-python-ldap-library-and-binding-to-an-ldap-directory)