#summary Various samples of code.
#labels Phase-Support


# Code Snippets #

This is a collection of miscellaneous code samples. Find various topics on the subpages to help you get aquainted with tryton coding.

## Define a many2many field ##

For defining a many2many field, you a) need an additional table / model b) define the field. First define the additional model to hold the relation:
```
class PartyWorksForParty(ModelSQL):
    'Define Party - Party relations'
    _name = 'party-worksfor-party'
    person = fields.Many2One('party.party', 'Person',
                             select=1, required=True)
    org = fields.Many2One('party.party', 'Organisation',
                          select=1, required=True) 

PartyWorksForParty()
```

Now define the many2many field  which uses the above relation:

```
class Party(ModelSQL, ModelView):
    _name = 'party.party'
    # this field related person -> organization
    works_for = fields.Many2Many('party-worksfor-party',
                                  'person', 'org',
                                 'Works for')
    # here is another field for relating organization -> person
    workers = fields.Many2Many('party-worksfor-party',
                               'org', 'person',
                               'Workers')
```

## Access the target of a many2many field ##

Assume some many2many field as defined in [#Define\_a\_many2many\_field](#Define_a_many2many_field.md). Now you can access the "target" side of the many2many relation like this:
```
        for party in self.browse(cursor, user, ids, context=context):
            res[party.id] = ', '.join(p.name for p in party.works_for)
```
As you can see, `party.works_for` is a list.

## tryton jsonrpc client for create a database ##

```
from jsonrpclib import Server as ServerProxy
import jsonrpclib
import json
import pprint

server = ServerProxy("http://localhost:8000", verbose=0)
try:
    server.common.db.list(None,None)
    a = json.loads( jsonrpclib.history.response)
    pprint.pprint(a["result"])
    server.common.db.create(None,None,'new_database_name',"password tryton admin","es_ES","admin_password")
except TypeError:
    a = json.loads( jsonrpclib.history.response)
    print "error:"
    print a["error"]

```

extended example: https://gist.github.com/1290571