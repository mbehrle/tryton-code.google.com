#summary Tips for bulk-importing data into Tryton
#labels Phase-Support

# Export/Import Limitations #

Due to the underlying models the csv Export/Import functionality is not always suited to provide a direct re-import of exported data. Have a look at http://groups.google.com/group/tryton/browse_thread/thread/1ee2fd4e21680d76 for an explanation of the details.

In conclusion, the import/export was not design to import the exported data.
It was design to export data for external purpose and to import data from
external sources.

# Importing Data via CSV #

## Selection fields ##
For selection, you must set the internal value (It could be improved to use
the translated value if internal doesn't match)

## one2many fields ##
You can import one2many entries like this:
```
party,purchase_date,lines/type,lines/product,lines/quantity,currency
Supplier,2009-04-26,line,Product A,1,Euro
,,line,Product B,2
,,line,Product C,3
```

Examples for one2many fields are party contact-mechanisms and invoice lines.

## many2one ##

For many2one, you must set the value of `rec_name`. Tryton will use the first found record that has the same `rec_name`.

```
name,parent
Parent Category,
Child 1,Parent Category
Child 2,Parent Category
Grandchild 1,Parent Category / Child 2
Grandchild 2,Parent Category / Child 2
Child 3,Parent Category
Grandchild 2,Parent Category / Child 3
```

Examples for many2one are categories, which build a hierarchy.

## many2many ##
For many2many, it works like many2one except that it allow many values separated by comma.