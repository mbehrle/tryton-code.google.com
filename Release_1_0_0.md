#summary Goals for release 1.0.0
#labels Phase-Requirements,Phase-Implementation,Phase-QA

# Overview #

  * Version number: 1.0.0
  * Estimated release date: [2008-11-17](http://www.tryton.org/community/calendar.html)
  * General topics for all releases are collected on [ReleaseGeneral](ReleaseGeneral.md)

# Todo #

  * Wiki for module documentation (with mercurial and sphinx)
  * ~~Add service company on website~~
  * ~~Add technical requirement on website~~ see TechnicalRequirements
  * ~~Use the "Application Platform" to describe Tryton~~
  * ~~Make the repository of the website public~~
  * Add features list for the platform on website
  * Add features list for principal modules on website
  * Write standard news for the release
  * Adding a manifesto for the Tryton community
  * ~~Test access rights~~

## Tests ##

> Please contribute the testing results in the matrix [Testing1\_0\_0](Testing1_0_0.md)

## trytond: Application platform ##

  * Technical documentation
  * ~~Add README~~

## tryton: Client ##

  * ~~Remove glade file~~
  * ~~Add README~~

## Modules: ##

### account\_be ###

  * Add missing accounts
  * Add taxes

### account\_statement ###

  * Handle invoice reconciliation

### party ###
  * ~~Change namespace to party~~
  * ~~Divide address from other contact mechanisms like phone/email/mobile/URL...~~
    * ~~two one2manys: one for address and one for contact~~