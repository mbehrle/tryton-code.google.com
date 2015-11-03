

# Introduction #

This document will provide propositions to replace current request by a real email system.
The goal is to store emails in Tryton and be able to read it with most email client.

Module Name: electronic\_mail

# MUA Incoming Protocol #

[Mail User Agent](http://en.wikipedia.org/wiki/Mail_User_Agent)
According to [Wikipedia](http://en.wikipedia.org/wiki/Mail_User_Agent#Standards), there is two popular protocols [POP3](http://en.wikipedia.org/wiki/POP3) and [IMAP4](http://en.wikipedia.org/wiki/IMAP4). IMAP4 will be chosen because it was designed to leave email on the server and it allow multiple clients to access the same mailbox.
The IMAP4 server will be implemented using [TwistedMail](http://twistedmatrix.com/trac/wiki/TwistedMail)

## Authentication ##

For the authentication, we need to know on which database the connection must be authenticated. We choose to store the database name in the login like this `username@databasename`.

# MDA #

[Mail Delivery Agent](http://en.wikipedia.org/wiki/Mail_delivery_agent)
It will be a simple python script that will work like [procmail](http://en.wikipedia.org/wiki/Procmail) but it will store the email into Tryton instead of mailbox.

# Storage Structure #

  * electronic\_mail.mailbox
    * name: char
    * user: many2one res.user
    * parent: many2one electronic\_mail.mailbox
    * subscribed: boolean
    * read\_users: many2many res.user
    * write\_users: many2many res.user
    * view: many2one electronic\_mail.mailbox (replace this mailbox content by an other one)

  * electronic\_mail
    * mailboxes: many2one electronic\_mail.mailbox
    * from: char
    * sender: char
    * to: char
    * cc: char
    * bcc: char
    * subject: char
    * date: datetime
    * message\_id: char
    * in\_reply\_to: char
    * headers: one2many electronic\_mail.header
    * digest: char(32) md5 of email without header depending of receipt like 'X-Original-To', 'Delivered-To'
    * collision: integer
    * email: function(binary) email from data\_path and header
    * flag\_seen: boolean
    * flag\_answered: boolean
    * flag\_flagged: boolean
    * flag\_deleted: boolean
    * flag\_draft: boolean
    * flag\_recent: boolean
    * size: integer

  * electronic\_mail.header
    * name: char
    * value: char
    * email: many2one electronic\_mail

# Links #

[Lamson](http://lamsonproject.org/)

# Update #

This blueprint has been partially implemented as follows:

  * [electronic-mail](https://github.com/openlabs/electronic-mail)
  * [electronic-mail-template](https://github.com/openlabs/electronic-mail-template)