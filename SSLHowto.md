#summary SSL Howto
#labels Phase-Deploy,Featured

# Howto activate SSL connection #

Tryton can be configured to use encrypted communication for all of its client protocols:
[JSON-RPC](https://en.wikipedia.org/wiki/JSON-RPC), [XML-RPC](http://en.wikipedia.org/wiki/Xmlrpc) and [WebDAV](http://en.wikipedia.org/wiki/Webdav). Each of these communication channels can be switched to use [SSL](http://en.wikipedia.org/wiki/Secure_Sockets_Layer).

Otherwise an eavesdropper would be able to intercept an unencrypted channel and get usernames and passwords.

## Dependencies ##

You need to have this package installed on both systems (server, client):

  * [OpenSSL](http://www.openssl.org/)

And this one on server:

  * [pyOpenSSL](http://pyopenssl.sourceforge.net/)

## Generate a self-signed certificate ##

If your organization does not have set up a PKI, or if you are only setting up a test system, you may get along with a self-signed certificate. If you are looking for a place to get "real" certificates, please visit http://www.cacert.org.

You can generate a self-signed certificate with this command on the server:

```
openssl req -new -x509 -keyout /path/to/private/server.pem -out /path/to/certs/server.pem -days 365 -nodes
```

## Configure the server ##

You must edit the configuration file (see the [documentation](http://doc.tryton.org/)).

You must restart the server.

## Use it ##

  * For the tryton client, there is no need to change anything. The client will use the SSL connection automatically and display a closed lock in the lower right corner.
  * For WebDAV access you need to change the schema (first part of the URL) to `webdavs://` (that is: append an `s`), while still using the same port.
  * For XML-RPC  you need to change the schema (first part of the URL) to `https://` (that is: append an `s`), while still using the same port.