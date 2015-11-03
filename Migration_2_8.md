# Migration from 2.6 -> 2.8 #

## MUST ##

  * `create()` requires a list of dictionaries.
  * `_inherits` support has been dropped.

## DEPRECATED ##

  * Use of `_constraints` is supported but should be replaced with `validate()`.