# Introduction #

This document outlines a proposal to add an Asset concept in Tryton not necessarily linked to accounting but that allows describing assets in the real world.

# Rationale #

It is necessary for a number of use cases to be able to introduce in the database real-world assets. Some use cases would include the  implementation of a CMMS (http://en.wikipedia.org/wiki/Computerized_maintenance_management_system), an IT Asset Management solution (http://en.wikipedia.org/wiki/IT_asset_management) or a Fleet Management Software.

So the developments discussed here aim to be as generic as possible so later can be reused.

An important aspect will be how those assets will be linked to account assets and probably stock lots because both objects already exist in Tryton and are quite similar in concept.

# Proposal #

## asset module ##

```
class AssetType:
    name = fields.Char(translate=True)
    icon = fields.Selection(translate=False)
    attributes = fields.Many2Many('asset.attribute-asset.type-set')


class AssetAttribute(DictSchemaMixin):
    types = fields.Many2Many('asset.attribute-asset.type-set')


class AssetAttributeAssetType:
    attribute = fields.Many2One('asset.attribute', 'Attribute', required=True)
    type = fields.Many2One('asset.type', required=True)


class Asset:
    name = fields.Char
    code = fields.Char(required=True, readonly=True) # Unique
    type = fields.Many2One('asset.type', required=True)
    active = fields.Boolean('Active')

    notes = fields.Text('Notes')
    icon = fields.Function(fields.Selection())
    attributes = fields.Dict('asset.attribute', 'Attributes',
        domain=[
            ('types', '=', Eval('type')),
            ], depends=['type'])
```


## asset\_relationship module ##

The asset\_relationship module would be mostly the same as the party\_relationship but linking assets instead of parties.

```
class Asset:
    relations = fields.One2Many('asset.relation.all')

class AssetRelation:
    from_ = fields.Many2One('asset', required=True)
    to = fields.Many2One('asset', required=True)
    type = fields.Many2One('asset.relation.type', 'Type', required=True)


class AssetRelationAll:
    # Just like PartyRelationAll
```

# Discusion #

https://groups.google.com/d/msg/tryton-dev/VAj1hoTCwh4/TGbVQFzJl68J


# Implementation #

asset: http://codereview.tryton.org/5781002

asset\_attribute: http://codereview.tryton.org/9871002

asset\_relationship: http://codereview.tryton.org/14691002