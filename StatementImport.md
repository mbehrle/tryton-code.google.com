

# Introduction #

Tryton already provides the account\_statement module but it lacks any infrastructure for importing bank statements. Given that there are tens or hundreds of different formats the module should only provide the basis in terms of data model and functionalities to store imported data and link it with the current statement model.

# Objectives and Features #
  * Store the bank statement keeping the same data provided by the bank
  * Rule system to ease and automate the process of finding invoices and reconciliation or determining accounts to use
  * Rule system should be extensible
  * Allow reverting and redoing the process by bank statement line => Full traceability of information from statement lines to imported (bank provided) statement lines.
  * Independent of file format
  * Manage duplicate lines if dates or lines of two imported files overlap

# Implementation #

Module name: `account_statement_import`

## Models ##

### `account.statement` ###

  * `imported_lines`: one2many with `account.statement.imported.line`
  * `imported_attachment`: many2one with attachment
  * `import_attachment`: Action that clears `imported_lines` and fills it with the data from the `imported_attachment`

The process should provide functions to automatically detect the file type and then import fill the `imported_lines` depending on the format.

### `account.statement.imported.line` ###

  * `name`
  * `statement`
  * `date`
  * `description`
  * `amount`
  * `lines`
  * `attributes`
  * `state`
  * `duplicates`
  * `valid_duplicate`

### `account.statement.imported.line.attribute` ###

  * `line`: many2one with `account.statement.imported.line`
  * `type`: selection
  * `value`: char/text

## Wizards ##

### `account.statement.import.file` ###

Allows the user to select a file to import