# Introduction #

This document exposes the benefit of having actions at field level and proposes a technical solution.


# Rationale #

Tryton already provides a very good navigation system from one record to its related ones by means of the green arrow in the toolbar. Those relations as well as the actions and reports in a party.party form can be reached from within an invoice by right clicking on its party field. This works very well but only works with relation fields, such as `Many2One`.

There are cases, however, where such functionality would be interesting in non-`Many2One` fields, specially in Function ones, where the user would like to know the details about an aggregated value. Good examples would be the "Receivable" and "Payable" decimal fields added to party.party form by the account module. The following proposal, would allow the user to right click on those fields and drill down to the account move lines that are used to calculate the value shown.


# Details #

A new function would be added to `ModelView` which would receive the list of fields for which the actions are requested and it would return a dictionary with field names as keys and the values are a dictionary like the one returned by `view_toolbar_get()`.

The following would be (more or less) the implementation in `ModelView`:

```
@classmethod
def fields_menu_get(cls, fields):
    res = {}
    for field in fields:
        keywords = []
        if isinstance(cls._fields[field], fields.Many2One):
            model_name = cls._fields[field].model_name
            keywords += Pool().get(model_name).view_toolbar_get()
        f = 'keyword_%s' % field
        if hasattr(cls, f):
           keywords += getattr(cls, f)('print')
           keywords += getattr(cls, f)('action')
           keywords += getattr(cls, f)('relate')
        keywords.sort(key=itemgetter('name'))
        res[field] = keywords
    return res
```

This would allow models to override `fields_menu_get()` although the most appropriate would be to add a per-field function:

```
@classmethod
def keyword_receivable(cls, keyword):
   pool = Pool()
   Action = pool.get('ir.action')
   ModelData = pool.get('ir.model.data')
   keywords = []
   if keyword == 'relate':
      action_id = ModelData.get_id('account', 'act_move_line_form')
      keywords += Action.get_action_values('ir.action.act_window', [action_id])
   return keywords
```

# To consider #

Should we support all keywords or only relate ones?