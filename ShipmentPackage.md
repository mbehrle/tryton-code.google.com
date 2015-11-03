# Introduction #

This document will explain the proposed `stock_package` module.

# Rational #

It is to allow to store packaging information about outgoing shipment (maybe also incoming?).
The packaging information should be designed by a tree structure as boxes could be inside other boxes which could on pallet etc.
The module should allow to print labels for each package.

# Details #

## Models ##

### 'stock.package' ###

  * 'type': many2one to 'stock.package.type'
  * 'shipment': reference to 'stock.shipment.out' or 'stock.shipment.in.return'
  * 'moves': many2many to 'stock.move' (with dynamic domain to prevent to pick twice the same move and a unique constraint)
  * 'parent': many2one to 'stock.package'

### 'stock.package.type' ###

  * 'name'

### 'stock.shipment.out', 'stock.shipment.in.return' ###

  * 'packages': 'one2many' to 'stock.package'

## Reports ##

A report to print all packages of a shipment with:

  * shipment code
  * package rec\_name
  * ~~if first level, shipment party, address etc.~~

## Implementation ##

http://codereview.tryton.org/1221003