# Notes #

  * A thread explaining some issues when creating new records: https://groups.google.com/d/topic/tryton-dev/WsiFFJa8Rh4/discussion

# To be improved #

  * Replace fields.Property with function fields that pick the value from a table depending on current company.
  * Translatable fields. The solution could be similar to properties but it may be harder because of the need to manage translation files.
  * Improve create() to not request default values for Function fields.

# Tips #

  * Ensure you store configurations. Not doing so, makes the system retrieve default values all the time which is much less inefficient.

# Cache #

Tryton has a built-in cache layer which is transparent for programmers but it is useful to have some knowledge on the way it works.

In both search() and browse() operations Tryton will cache some information (that of the fields marked as loading=eager) and cache will be invalidated on write/save operations.