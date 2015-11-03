


# Introduction #

> Materials resource planning(MRP I) strives to prevent stockouts by allocating the necessary materials so that the production process can successfully produce the products in demand.  The successor of MRP I is MRP II (manufacturing resource planning). MRP II strives to prevent stockouts, improve efficiency and reduce costs by compounding the resource planning done in MRP I with planning the production process itself (ie. scheduling, machines, finances, human elements, capacity planning).

For example:
  * sales orders are processed into production orders;
  * productions orders trigger material allocation and the release of work orders to the shop floor;
  * work orders arrive at workcenters and allow each operation of the routing to be performed in sync with the overall production plan.

An MRP system should also be able to forecast demand based on previous sales to predict the best time for production. In the best of all worlds the MRP system would determine what workcenters build what and when based on what would fit real and predicted demand.

This document has the following two goals: first to document most of the common features found in MRP(I/II) systems and second to narrow down the most important features for the first milestone of the implementation.


# Road Map #
## Milestone One ##
  1. Implement a BOM model that supports modular and phantom bom types. See figure 2.
  1. Create a view to access BOM data under product based off "producable" checkbox (like purchasable and salable).
  1. Create a production order model.
  1. Create a main menu entry for Production Management with a submenu entry for production orders.  Under production orders there will be a quick-access entry to lists of production orders for each of the following states: draft, assigned, running and stopped.
  1. The actions taken between production order state changes move production materials(products) from storage through the production area and moves the finished products to the production output zone and back into storage.  A production order will take on the following states: Draft, Assigned, Running, Finished, Done, Stopped and Canceled. See Figure 1.
  1. A sales orders can trigger the creation of draft production orders if the product is produceable and not in stock.
  1. Create a Configurable BOM Model that can be propagated to standard BOMs.  The dependent BOMs need to be able to be made read only in the regular BOM editor.
  1. Create a Configurable BOM Designer that will be listed off of the Production Management menu item.
  1. Modify the Sale Line interface to allow use of the Configured Product Finder.
  1. Create a Product Configurator that uses a configurable BOM to create many products each with their own "configured" BOM.  Future changes to the configurable BOM will be propagated to each "configured" BOM as necessary to maintain validity.

## Milestone Two ##
  * basic production planning (Similar to MRP I)

## Milestone Three ##
  * advanced production planning (Similar to MRP II)
  * capacity planning
  * shop floor scheduling using routings and workcenters

# Feature List #

## Production Module(production) ##

A BOM will have one or more BOM Inputs with each BOM Input referencing a product, a quantity and a UOM. (Single level BOM)

A BOM will have one or more BOM Outputs with each BOM Output referencing a product, a quantity and a UOM.  (Multiple output BOM)

One or more BOM Outputs will be marked principal, meaning they can be used to produce the product referenced by that BOM Output.  This will be used to aid in selecting a BOM to use to produce a product specified by a Production Order.

Every product will have a sequence number to give priorities to all BOMs that define it as a BOM output.  This can be used to select a BOM for a product as well as to select the default BOM. ( I have no idea where this will live and how it will be kept up to date )

A BOM must be selected for a product listed on a Production Order when the Production Order is in the Draft state.  Once the state of the production order has changed the selected BOM(s) cannot be changed.

A BOM can have 1 or more revisions.

A production order has a planned date, a product, a planned quantity, a uom, a specific BOM revision for that product and any product's BOM in the top-level bom's tree , an actual start date, an actual done date, an actual quantity and a state.  If a product is configurable its configuration will also be included.

A production order will have the following states: Draft, Assigned, Running, Finished, Done, Stopped, Canceled.

Inventory is assigned to a production order and moved to the production input zone when a production order changes from Draft to Assigned, this can be forced.

Inventory is moved to consumed when a production order changes from Assigned to Running.

Inventory is moved to the production output zone when a production order changes from Running to Finished.

Inventory is moved to Storage when a production order changes from Finished to Done.

Inventory moves are canceled between Storage and the Production Input Zone when a production order changes from Assigned to Draft.

Inventory moves are canceled between the Production Input Zone and Consumed when a production order changes from Running to Stopped.

Inventory moves are canceled between Storage and the Production Input Zone and/or Consumed when a production changes from anything other than Finished, Done or Canceled.

A production order with state Finished, Done or Canceled is read-only.

## Product Substitutes Module(production\_substitutes) ##

A BOM Input can have a list of substitute BOM Inputs, this functionality will be used during the assigning of stock from storage prior to starting production.

A Product can have global substitutes, these will be specified on the production tab of the edit product view.  This functionality will be used during the assigning of stock from storage prior to production.  This functionality can be overridden by specifying a BOM Input as not globally substitutable.

Substitute BOM Inputs as specified either locally or globally can be selected either manually or automatically when moving the Production Order from Draft to Assigned using a wizard.

## Phantom Subassembly Module(production\_phantoms) ##

A product can be created to be used as a phantom subassembly which allows it to be produced on the production line without generating another production order.

Pulling phantom sub assemblies from stock can be manually or automatically done during the assignation process.

## Configurable BOM Module(production\_configurations) ##

A configurable BOM is similar to a normal BOM except inputs can be grouped and the integers L, M and N can be specified such that a choice of L to M choices can be made from the N inputs in the group.  No outputs are defined in a configurable BOM.(Configurable BOM)

A configurable BOM will be defined with the Configurable BOM Designer.

A configurable BOM can be configured with the Configurable BOM Configurator to create a BOM(a normal bom as mentioned above, but it is read only from the normal BOM interface and can only be edited through the configurator).   A configured BOM also can only have a single output.  The output will be principal and there will be no by-products.

A Configured BOM Finder can be used to find a specific BOM configuration and the product it defines.  This is done by starting with the configurable bom and selected choices as was done in the Configurator except with intent to match the configuration to existing configured BOMs (Probably need to resolve how this works to find products versus their boms)

## Basic Production Planning(production\_mrp) ##

Produceable products can set a lot sizing method for use during planning.

A Master Production Calendar(MPC) will consist of these elements: Begin and End dates, a finite number of periods, a period size(year/month/week/day), an initial inventor\
y for each product, and a demand forecast for each product for each period.

The periods can be automatically created based on the period size and begin/end dates.(Similar to Fiscal Year)

Product demand can be automatically estimated from previous sales for each period.

The Master Production Calendar can be used to create a Master Production Schedule which consists of Purchase Requests and Draft Production Orders for each period of the C\
alendar.  These must be satisfied by Purchases or by Production Orders respectively.

## Shop Floor Control(production\_sfc) ##

A workcenter has a name, description and capacity details.

A workcenter group consists of one or more workcenters and is used to given a routing plan more flexibility.

A routing plan is a list of operation plans each which can be performed at a specific workcenter or any workcenter in a specified group.  An operation plan has a descript\
ion, a setup time, a cleanup time, a lead time, resource requirements(allocation from elsewhere, ie. people/tools) and capacity requirements.

A routing plan can have 1 or more revisions.

A product can have one primary routing plan revision associated with it.

A production run can be scheduled at workcenters based on the primary routing plan revision associated with the product to be produced using the assign/force assign parad\
igm with regards to capacity and usage conflicts.

## Shop Floor Control(production\_capacity) ##

Finite capacity planning can be used to check routing schedules.

## Disassembly of products ##

A product can be disassembled to its original parts(products) based on a BOM selected by a user.

The parts(products) will be returned to their default stock location unless that is customized by the user.

A wizard will exist to allow the user to select the BOM as well as customize the destination locations for returning the parts(products) to storage.

BOMs can be marked to be either available for use in disassembly or not available for use in disassembly.  Such functionality would probably be restricted to the same level of authorization as the modifications of the bom itself.

The user will be able to "prune" the product's BOM in order to disassemble a product into one or more subassemblies rather than the raw materials/simplest parts. More explicitly the user will be able to select one or more products in the multi-level BOM that will not be recursively disassembled. **mm**

Futhermore BOMs could also be marked as to whether disassembly was the default action to take.  This would default to YES they should always be disassemblied.  This could be overriden in the wizard in the event that a user wanted a subassembly in that case. **mm**

A user could specify a location for all the parts to be shipped to during disassembly. **mm**

**mm** These features would probably need to be in separate modules.

## Unassiged ##

A product kit may consist of two or more existing products. (Product kits) **oo**

A list of current product within a product that has been deployed or serviced may be maintained. (Inventory Item Configurations) **oo**

A BOM may exist for engineering and/or manufacturing. **oo**

**oo** These items need to be more specific.

# Prototypes #

## Model ##

http://mercurial.intuxication.org/hg/production

http://mercurial.intuxication.org/hg/production_substitute

http://mercurial.intuxication.org/hg/production_phantom

http://mercurial.intuxication.org/hg/production_configurable


# Figures #


http://www.laspilitas.com/tryton/production-inventory-layout.png?size=grid24_24

-1- _Caption: Proposed production inventory layout.  (Until I can upload this I'm just linking off to it)_


http://www.laspilitas.com/tryton/demo-bom.png?size=grid24_24

-2a- _Caption: Demonstration of the BOM functionality to be implemented. (Until I can upload this I'm just linking off to it)_

http://www.laspilitas.com/tryton/configurable-bom.png?size=grid24_24

-2b- _Caption: Demonstration of the Configurable BOM functionality to be implemented. (Until I can upload this I'm just linking off to it)_

|Inputs|| | | | | | | |
|:-----|:|:|:|:|:|:|:|:|
|Product|Qty|UOM|Choice-Slot|Choose-Min-No|Choose-Max-No|Sub-Slot|Allow-Global-Sub|
|ACME Case/Pwr/Mbrd|1|Unit|-|-|-|-|Yes|
|ACME Memory 1GB|2|Unit|-|-|-|1|Yes|
|ABC Memory 1GB|2|Unit|-|-|-|1|-|
|ACME Hard Drive 80GB|1|Unit|1|1|1|-|Yes|
|ACME Hard Drive 160GB|1|Unit|1|-|-|-|Yes|
|ACME CPU 3.0 Ghz CPU|1|Unit|2|1|1|2|No|
|ABC CPU 2.8 Ghz CPU - Large FSB|1|Unit|-|-|-|2|-|
|ACME CPU 3.2 Ghz CPU|1|Unit|2|-|-|-|Yes|
|ACME CPU 3.4 Ghz CPU|1|Unit|2|-|-|-|Yes|


Notice that 6(given by 2\*3) different BOMs can be configured from this Configurable BOM.  Those BOMs are as follows:


|Inputs|| | | | | |
|:-----|:|:|:|:|:|:|
|Product|Qty|UOM|Sub-Slot|Allow-Global-Sub|
|ACME Case/Pwr/Mbrd|1|Unit|-|Yes|
|ACME Memory 1GB|2|Unit|1|Yes|
|ABC Memory 1GB|2|Unit|1|-|
|ACME Hard Drive 80GB|1|Unit|-|Yes|
|ACME CPU 3.0 Ghz CPU|1|Unit|2|No|
|ABC CPU 2.8 Ghz CPU - Large FSB|1|Unit|2|-|

|Inputs|| | | | | |
|:-----|:|:|:|:|:|:|
|Product|Qty|UOM|Sub-Slot|Allow-Global-Sub|
|ACME Case/Pwr/Mbrd|1|Unit|-|Yes|
|ACME Memory 1GB|2|Unit|1|Yes|
|ABC Memory 1GB|2|Unit|1|-|
|ACME Hard Drive 80GB|1|Unit|-|Yes|
|ACME CPU 3.2 Ghz CPU|1|Unit|-|Yes|

|Inputs|| | | | | |
|:-----|:|:|:|:|:|:|
|Product|Qty|UOM|Sub-Slot|Allow-Global-Sub|
|ACME Case/Pwr/Mbrd|1|Unit|-|Yes|
|ACME Memory 1GB|2|Unit|1|Yes|
|ABC Memory 1GB|2|Unit|1|-|
|ACME Hard Drive 80GB|1|Unit|-|Yes|
|ACME CPU 3.4 Ghz CPU|1|Unit|-|Yes|


|Inputs|| | | | | |
|:-----|:|:|:|:|:|:|
|Product|Qty|UOM|Sub-Slot|Allow-Global-Sub|
|ACME Case/Pwr/Mbrd|1|Unit|-|Yes|
|ACME Memory 1GB|2|Unit|1|Yes|
|ABC Memory 1GB|2|Unit|1|-|
|ACME Hard Drive 160GB|1|Unit|-|Yes|
|ACME CPU 3.0 Ghz CPU|1|Unit|2|No|
|ABC CPU 2.8 Ghz CPU - Large FSB|1|Unit|2|-|

|Inputs|| | | | | |
|:-----|:|:|:|:|:|:|
|Product|Qty|UOM|Sub-Slot|Allow-Global-Sub|
|ACME Case/Pwr/Mbrd|1|Unit|-|Yes|
|ACME Memory 1GB|2|Unit|1|Yes|
|ABC Memory 1GB|2|Unit|1|-|
|ACME Hard Drive 160GB|1|Unit|-|Yes|
|ACME CPU 3.2 Ghz CPU|1|Unit|-|Yes|

|Inputs|| | | | | |
|:-----|:|:|:|:|:|:|
|Product|Qty|UOM|Sub-Slot|Allow-Global-Sub|
|ACME Case/Pwr/Mbrd|1|Unit|-|Yes|
|ACME Memory 1GB|2|Unit|1|Yes|
|ABC Memory 1GB|2|Unit|1|-|
|ACME Hard Drive 160GB|1|Unit|-|Yes|
|ACME CPU 3.4 Ghz CPU|1|Unit|-|Yes|

-3- _Caption: Tables demonstrating a configurable BOM and its configured BOMs._



http://www.laspilitas.com/tryton/production-order-states.png?size=grid24_24

-4- _Caption: Production order state transition diagram. (Until I can upload this I'm just linking off to it)_



http://www.laspilitas.com/tryton/bom-er.png?size=grid24_24

-5- _Caption: Entity Relationship diagram reflecting how boms and associated structures relate._