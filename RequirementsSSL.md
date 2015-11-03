#summary Requirements for SSL implementation
#labels Deprecated

# Objectives #

[Wikipedia](http://en.wikipedia.org/wiki/Transport_Layer_Security#Description) about SSL (TLS):

> The TLS protocol allows client/server applications to communicate across a network in a way designed to prevent eavesdropping, tampering, and message forgery. TLS provides endpoint authentication and communications confidentiality over the Internet using cryptography.

SSL can only prevent eavesdropping (etc.) if it is not only used to set up an encrypted channel. But it is most important to verify whom the client is talking to -- this is: the server needs to authenticate itself to the client. Otherwise an intruder could simply present a fake certificate an intercept the communication. Confidentiality is gone!

One of the major problems of SSL implementations (in web-browsers) are users ignoring warnings about wrong certificates (which means: you are talking to the wrong server) or accepting non-SSL connections where a SSL-connection would be required (this is: talking unencrypted). Thus Tryton is either set up to use SSL, not to not use it. If Tryton is configured to use SSL, there must be no (auto-) magick fall back to non-SSL, and the client must authenticate the server. Everything else is insecure and grossly negligent.

# Requirements #

  * ~~Communication via SSL is optional.~~ (done)
  * ~~SSL may be activated for each communication type separately: netrpc, xmlrpc, webdav, ...~~ (done)
  * If SSL is activated of a communication type, it becomes mandatory for this communication type. This is:
    * ~~The server **must not** fall back to non-SSL for these communication types, but raise a server error.~~ (done)
    * The Tryton client **must not** fall back to non-SSL communication, but deny connection for known server with SSL certificate.
  * ~~The Tryton client should display an icon in the status-bar to indicate SSL is active (no icon if SSL is inactive).~~ (done)

  * SSL version must be configurable on the server.

## Certificate Checks ##

  * The same certificate is used for all communication types. Since all services are running on the same server, there is no use for different certificates.
  * The client must store certificate by DNS name.
  * The client must ask to the user to store a new certificate. It must display all the informations available on the certificate and display a warning for non-trusted CA certificate.
  * The client must check the validity of the certificate and refuse connection if expired.
  * The client must refuse connection if the certificate has changed between connections with the exception of expired certificate.
  * The user can force the update of a certificate after a warning.

# Implementation #

To be written after requirement are agreed.

# Links #

  * [python-nss](http://fedoraproject.org/wiki/Features/PythonNSS)