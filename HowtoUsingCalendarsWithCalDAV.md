#summary CalDAV/CardDAV with Tryton


# How to use Calendars with CalDAV #

Tryton supports a service for calendars to be accessed using CalDAV protocol.

## Install Calendar Module and create a Calendar ##

To add calendar services to Tryton, proceed as follow:

  * Install the following Tryton modules:
    * calendar
    * calendar\_todo (optional)
  * Go to Calendar > Calendar
  * Create a new calendar
  * Calendar Owner can be all users which have an email address. (If you can't find any of your users, check in Administration > User > User, if the email adresses for each user are set.)
  * On tab security you can give permissions to other tryton users.

## Connecting with Sunbird/Iceowl 0.9 ##
  * Install Sunbird/Iceowl as described [here](FIXME.md)

  * You can now access the calendar from your CalDAV application using the URL `http://<server:port(8080)>/database/Calendars/<calendarname>`. The user needs to authenticate herself.

Notes:
  * You may prefer secure communication using HTTPS (HTTP over SSL). Please refer to [SSLHowto](SSLHowto.md) for mor information how to set up Tryton with SSL. The URL will start with `https://...` obviously.
  * Make sure you have an up to date version of the Python package 'vobject' installed. You need at least > 0.6.

# How to use Contacts with CardDAV #

  * Access to the parties of a Tryton database is provided by the URL `http://<server:port(8080)>/database/Contacts`. The user needs to authenticate herself.

# Working setups #
A collection of working/not working setups can be found at http://spreadsheets.google.com/pub?key=tcP37m3wxUAUC_pxct2xYqQ&output=html