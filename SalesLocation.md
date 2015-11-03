# Sales Location: #

## Introduction ##

For some companies it's very important to manage different sale locations  because many of them has different shops. With this module we can have         a default shop per user.

Default values for sale fields, based on shop selection
  * Default invoice method
  * Default shipment method
  * Default pricelist
  * Default payment term
  * Default warehouse
  * Default party

## Objectives and Features ##

A lot of Tryton Collaborators has their own module of Shop, this
Blueprint is to try to unify in a Tryton way to make better code.

## Implementation ##

We base in the implementation of Zikzakmedia https://bitbucket.org/zikzakmedia/trytond-sale_shop/src

## Models ##

sale.shop (or sale.location)

  * Shop Name - mandatory
  * Company (relation many2one) - mandatory
  * Sale Reference Sequence (relation many2one)
  * Sale Invoice Method (relation selection)
  * Sale Shipment Method (relation selection)
  * Pricelist (relation many2one)
  * Payment terms (relation many2one)
  * Warehouse (relation many2one)
  * Default Party (relation many2one)
  * User (relation many2many)

Some fields are not mandatory and they wont be used as default values in
sales.

res.user
  * Shops (relation many2many): The shops allowed to use by the user
  * Shop (relation many2one, domain=[('id', 'in', Eval('shops', [.md](.md)))] ): The default shop of the user

User can change his default shop in the "User preferences" view, like company or language.