#summary Goals for release 1.2.0
#labels Phase-Requirements,Phase-Implementation

# Overview #

  * Version number: 1.2.0

# Goals #

  * ~~Implement historical data (server and client side)~~
  * ~~Re-factorize OSV/ORM~~
  * ~~Improve XML-RPC for introspection~~
  * ~~Reconstruct the main windows of the client when the language changes~~
  * Split modules:
    * purchase -> purchase\_simple/base, purchase\_stock, purchase\_account
    * sale -> sale\_simple/base, sale\_stock, sale\_account
  * Configuration model (to store global configuration values in the database)
  * Add CardDAV interface
  * Add WebCal interface
  * Add JSON interface
  * Gantt chart in the client