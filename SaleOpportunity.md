#summary Events, Leads, Opportunities Management
#labels Deprecated

**Implemented**: [sale\_opportunity](http://hg.tryton.org/modules/sale_opportunity)

# Introduction #

The module helps to organise parties as Leads, Opportunities and Parties

# Details #

## Aim ##

This module implements a simple CRM framework allowing user to use the party itself as an entity to enter leads and opportunities.

## Objects & Fields ##

### crm.opportunity ###
  * party\_id: m2o party
  * date: date
  * title: char
  * description: text
  * stage: m2o: crm.opportunity.state
  * lines: o2m:opportunity lines
  * history: Use history feature of Tryton?
  * forecast\_value: float forecasted value

### crm.opportunity.lines ###
  * opportunity: m2o opportunity
  * product\_id: m2o product
  * quantity: float

### crm.opportunity.state ###
  * date: datetime
  * user: use the user field itslef?
  * state: Selection Lead, Opportunity, Confirmed, Cancelled, Lost
  * probability: 0%, 10%, 20%, 30% ... 90%, Hidden if not Opportunity
  * comment: Should it be required field?