

# General description #
Contracts are used in business system to manage long term relationships to customers. Contract or outline agreement contains basic information about the involved business parties and the business terms. In  pezial contracts can be used for periodic customer billing without separate sales order (similar to your telephone bill)

# Overview #
Customer contracts are outline customer agreements that are used when materials or services are sold within a certain time period.
## Contract categories ##
The following contract categories can be distinguished:

  * Master Contracts <br> The master contract is a document in which one can group contracts together as lower level contracts in a hierarchical manner. Thus, all the data that refers to other (underlying) documents remains consistent. The master contract contains the general terms which apply for all lower level contracts.</li></ul>

<ul><li>ServiceContracts <br> A service contract is an agreement that contains the conditions for offering a certain service to the customer. Typical examples are telecom or maintenance contracts. A service contract contains validity dates, cancellation conditions, price agreements, and information on possible follow-up actions.</li></ul>

  * Quantity Contracts <br> A quantity contract is an agreement that is used if a customer will order a certain quantity of a product from you during a specified period. The contract contains basic quantity and price information, but does not specify delivery dates or quantities.</li></ul>

<ul><li>Value Contracts <br> A value contract is a contractual agreement with a customer that contains the materials and/or services that they may receive within a time period and up to a target value. A value contract can contain certain materials or a group of materials (product hierarchy, assortment module).<br>
<h2>Models</h2></li></ul>

### contract.contract ###

Used to store diferent terms and conditions

  * Fields:
    * `name`: Translatable Char (Required)
    * `terms`: Many2One to contract.terms
    * `lines`: Many2One to contract.lines
    * `interval_type`: Selection ('day', 'week', 'month', 'year')
    * `interval\_number': Integer

Interval type and interval number are used to especify the duration of the contract. Interval\_number = 3, and interval\_type = 'month' represents a contract of 3 months

### contract.terms ###

Used to represent the terms and conditions of a contract

  * Fields:
    * `sequence`
    * `type`: Selection ('title', 'term', 'condition', 'comment')
    * `text`: Translatable Text

### contract.line ###

Used to represent the involved products of the contract

  * Fields:
    * `quantity`
    * `product`
    * `description`: Required

As in sale.sale, product is not required, but will be used to fill description

### contract.agreement ###

Used to represent the signature of a contract with a party

  * Fields:
    * `company`: Many2One to company.company
    * `party`: Many2One to party.party
    * `contract`: Many2One to contract.contract
    * `reference`: Char filled by a sequence
    * `start_date`: Datetime (required)
    * `end_date`: Datetime
    * `state`: 'draft', 'negotiating', 'active', 'canceled'

A report should be added to represent the agreement between the company and the party

# Detailed description #
## Master Contracts ##
The master contract is a document under which one can group other contracts as lower level contracts. It contains the general terms which apply for all the lower level contracts over a specified period.

Single contracts are grouped as lower level contracts under a master contract to ensure that

  * The terms in the master contract are granted in all the lower level contracts
  * The data in all lower level contracts remains consistent

It should be possible to group all all contract types under a master contract:

  * Quantity contracts
  * Value contracts
  * Service contracts

The link between the master and lower level contracts is controlled by assigning a new contract to an existing master contract. The relevant information from the master contract is copied into the newly created low-level contract. For this, the master contract contains only header data, like business data, partner information, contract data, billing data.

## Service Contracts ##
### General usage ###
Service contracts are used to record the details of the service package that companies have agreed to provide a service over a specified period of time. For example, this can specify:

  * The regular fees and services that are provided by you to a customer
  * The routine service tasks which are to be performed on a piece of machinery you have sold or rented to a customer
  * The prices which are to apply for these routine tasks.
  * The prices which are to apply for additional service tasks and for any spare parts required.
  * The terms under which the contract can be cancelled

During the validity period of the service contract, the contract is used as follows:

  * To initiate automatic billing of the routine service tasks at regular intervals (without additional sales order!)
  * To determine whether a service request from the customer is covered by the service contract (optional)
  * To determine which price agreements apply for service tasks not covered by the service contract
  * To determine whether a cancellation request from the customer is valid
  * To initiate follow-up actions before the service contract becomes invalid (I would see the CRM activity optional for the beginning)

### Billing intervals ###
Intervals should be set in each contract to week, month year or posting period
5.2.3Pricing
Pricing in Service contracts consists out of two components:

  * Standard pricing to determine the monthly fee for a service package. This can be defined via a material that represents the service package or a material group that covers a range of service items. <br> Example: The monthly fee for a telecoms line</li></ul>

<ul><li>Variable pricing for service materials that are applicable and used in the billing period. Quantity prices and volume rebates are applicable similar as in ordinary sales orders. <br> Example: additional charges apply for long-distance and international calls.</li></ul>

One or both elements are subject to
  * overall bonus agreements (once your turnover exceeds 10.000 EUR, you will get another 10% discount)
  * price scales according to material price definition
  * a commission for an agent that has arranged the deal. (This should result in one or more line items in a credit memo to the agent)

## Quantity Contract ##
### General usage ###
A quantity contract is an agreement that a customer will order a certain quantity of a product from you during a specified period. The contract contains basic quantity and price information but no schedule of specific delivery dates and quantities.

The customer fulfills the contract by placing sales orders against it (Call-off). If a sales order is created, it has to be created with reference to the outline agreement (the quantity contract). By this, tryton should update the quantities in the contract.
### Billing intervals ###
No billing intervals take place, billing should be per call-off.
### Pricing ###
Pricing is according to the underlying material, taking into account header and item information from the quantity contract.
## Value Contract ##
### General usage ###
A value contract is an agreement with a customer that contains the materials and services that the customer receives within a specified time period, and for a value up to a specified target value.

In the value contract you can refer to lists of materials that have already been defined (e.g. materials grouped within a material group or a hierarchical top-level material)

The customer fulfills a contract by placing sales orders against the contract. The contract does not contain any exact dates for deliveries, so the date information is covered inside the sales order.

By this, tryton should update the total order and delivery values in the contract. The call-off order value is calculated from the total of the open order and delivery values, plus the value that has already been billed to the value contract.

A value contract is complete when it either expires, or a reason for rejection is entered. Once the target value is reached, the tryton should issue a warning or an error, depending on the settings in the value contract header.
### Billing intervals ###
No billing intervals take place, billing should be per call-off.
### Pricing ###
Pricing is according to the underlying material, taking into account header and item information from the value contract.



# Discussion #

https://groups.google.com/d/topic/tryton/jXm7o73JxH0/discussion