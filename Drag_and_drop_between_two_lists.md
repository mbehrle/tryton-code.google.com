# Rationale #

Tryton current support of drag and drop allows to re-order or
re-parent items inside the same list.

The idea of this blueprint is to handle a generic drag and drop
between arbitrary lists. Those lists can be two x2many on the same
form view, two tree views inside a dashboard or even between two
different tabs.

There is two distinct situation. The first one is when the user drop records on a line (and so on an existing record). The other is when the user drop the records on a list view but not on a particular line (for example on an empty list or under the existing lines).


# DnD on a record #

A new model `ir.ui.view.droppable` allows to define which records
can be dropped on a record of a particular view. It contains the following
fields:

  * `model`: A char that contains a model name, E.G: `party.party` (required).
  * `condition`: A char that contains a Pyson expression.
  * `view`: A many2one that reference a tree view (required).

There is no unique constrain on `(model, view)` to allow any module to
extend the behavior.

A new one2many field `droppables` on `ir.ui.view` express the relation
supported by the `view` field.

When the client makes the `fields_view_gets call`, the server will
collect the droppables lines linked to the view and add a `droppable`
property on the view definition. The `droppable` property contains a
dictionary. The keys of this dictionary are the model and the values
are list of pysons expression.

So when the user starts to drag records, the client is able to know on
which list the user can drop them based on the model and the value of
the records. All the records must fit the Pyson expression to be
accepted.

When the records are dropped, the client will call the `on_drop` method
of the model that receive the records and will pass the model and ids
has arguments. The rpc class on the server will convert those
arguments into a list of records. So the `on_drop` method will look like
this:

```
class MyModel(ModelView):

    def on_drop(self, records):
        # Ideally the method should first test the model
        # of the records 
        for record in records:
            record.some_field = self
            record.save()
```

As this method must work on the correct values, the manipulated
records must be saved prior to be dragged or dropped.

After the `on_drop` called is finished, the client will reload the
records that where dragged and the record on which they are dropped.


# DnD on a list #

A new field `on_drop` on the view model defines which method must be called when the records are dropped.

Example of view definition:

```

        <record model="ir.ui.view" id="production_view_list_done">
            <field name="model">production</field>
            <field name="type">tree</field>
            <field name="name">production_list</field>
            <field name="on_drop">done</field>
        </record>
```

For reference, the done method is:

```
    @classmethod
    @ModelView.button
    @Workflow.transition('done')
    def done(cls, productions):
        pool = Pool()
        Move = pool.get('stock.move')
        Date = pool.get('ir.date')
        Move.do([m for p in productions for m in p.outputs])
        cls.write(productions, {
                'effective_date': Date.today(),
                })
```