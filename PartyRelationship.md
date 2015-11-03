# Introduction #

This document details the proposal of the new party\_relationship module.

# Rationale #

Tryton has support for managing parties but there is no way to relate them. For example, a customer and the accountant of that customer are both Parties in the system but the user can not establish a link between them.

This module tries to address this limitation.

# Details #

The module will add a new tab where all relationships are shown. That is if the user is in the Party form of an Accountant, the Accountant's company will be listed in its relationships tab (one2many field) with the "Accountant of" relationship shown. If the user is in the party of a company, the Accountant will be listed in its relationships tab with the "Accountant" relationship shown.

What it is special here is the need of handling both directions of the relationship in the Party view in a single One2Many widget. Note that not all relationships will be hierarchical (partner of, sibling of, are a couple of examples) so using two One2Many widgets would not be appropriate. To solve that, several Function fields are created.


## Models ##

### party.relation.type ###

This model stores the kinds of relationship between parties. For example: "employee of", "accountant of", "subsidiary of".

  * Fields:
    * `name`: Translatable Char
    * `reverse`: Many2One to party.relation.type

### party.relation ###

This model stores the relations between two given parties.

  * Fields:
    * `from`: required Many2One to `party.party`
    * `to`: required Many2One to `party.party`
    * `type`: required Many2One to `party.relation.type`.

### party.relation.all ###

Based on a SQL query similar to:

```
SELECT id * 2, from, to, type FROM party_relation
UNION
SELECT id * 2 + 1, to, from, r.type FROM party_relation JOIN party_relation_type AS t ON type = t.id JOIN party_relation_type AS r ON t.reverse = r.id
```

`create`, `write` and `delete` will be override to update the `party.relation` Model.

### party.party ###

  * Fields:
    * `relations`: (One2Many to `party.relation.all` with field `from`)

# Discussion #

https://groups.google.com/d/topic/tryton/jXm7o73JxH0/discussion