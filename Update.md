#summary Updating an existing database
#labels Phase-Design

# Introduction #
In case of changes in the framework or the modules, database update is required.

For updating the database, start trytond with the following command line:
```
# trytond -d <DATABASE_NAME> --all
```

Options:
  * -d DATABASE\_NAME: the database name to update.
  * --all: update all modules.
  * -u module: update only some modules like: `-u account company ir product`

The update process may take some times depending on the number of modules installed and the quantity of data in the database.

After the update, the server will stop. Then you can start it normally.


## Server messages explained ##

### E.g. Field password of 1@res.user not updated (id: user\_admin), because it has changed since the last update ###

The update process tries to take care about the users modifications.

This is made thanks to the table (ir.model.data) which keep the association with all the records defined in the modules xml-files and the corresponding records in the db.

This means that it is possible to edit the records created by the module installation and update it without being afraid of losing the handmade changes.

### E.g. INFO Field groups on res.user : integrity not tested. ###

Is a informational message about the field groups in object res.user.

Tryton can not test the integrity of the entries in groups, because groups create records on a specific table which handle the many2many relation, and there is no id in the xml corresponding to records in this table.

So its impossible for the update mechanism to check the integrity of of the values in the field groups.

Finally "integrity not tested" means that the module update will overwrite the field even if there was a modification, because it's not possible to find out if there was a modification for this record.

Conclusion: The update of this record was successful, but there is a possible risk of lost user modifications.