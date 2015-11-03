

**Implemented in series 1.7**

# Introduction #

This document will provide propositions to integrate into Tryton generic trigger functionality.

# Trigger Definition #

A trigger is linked to one model.
It will be run if its condition will be satisfied.
It will be possible to specify that a trigger can be run only once per model.
It will define trigger action.

## Trigger Conditions ##

A trigger will have a condition that will be evaluated to determine if the action must be executed.

On create, if the condition is evaluated to true after the creation then the action is executed.

On write, if the condition is evaluated to false before the write and to true after, then the action is executed.

On delete, if the condition is evaluated to true before the deletion, then the action os executed.

Example of condition:
|state == 'draft'|
|:---------------|
|amount > 1000   |
|parent.amount > 1000|

On time, the condition will be evaluated by a cron task.

Example of condition:
|now - create\_date > 3600|
|:------------------------|

## Trigger Action ##

It will define a model on which trigger will call a function with this signature:

```
       def fnct(self, cursor, user, model, ids, trigger_id, context=None)
         '''
         :param cursor: the database cursor
         :param user: the user id
         :param model: the triggered Model
         :param ids: the ids of the triggered record
         :param trigger_id: the id of the trigger record
         :param context: the context
         '''
```

## Trigger Model ##

```
class Trigger(ModelSQL, ModelView):
    _name = 'ir.trigger'

    name = fields.Char('Name', required=True)
    model = fields.Many2One('ir.model', 'Model', required=True, select=1)
    on_time = fields.Boolean('On Time', select=1, states={
            'invisible': Or(Eval('on_create', False), Eval('on_write', False),
                    Eval('on_delete', False)),
            })
    on_create = fields.Boolean('On Create', select=1, states={
            'invisible': Eval('on_time', False),
            })
    on_write = fields.Boolean('On Write', select=1, states={
            'invisible': Eval('on_time', False),
            })
    on_delete = fields.Boolean('On Delete', select=1, states={
            'invisible': Eval('on_time', False),
            })
    condition = fields.Char('Condition', required=True)

    action_model = fields.Many2One('ir.model', 'Action Model', required=True)
    action_function = fields.Char('Action Function', required=True)
```