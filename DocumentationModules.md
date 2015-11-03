#summary Guidelines and template for module documentation
#labels Phase-Requirements

# Introduction #
The target audience for module documentation are users of a specific Tryton implementation. Module documentation extends the general documentation of Tryton. It should not repeat, replace or re-phrase the contents of other documentation.

The documentation for each module should be very similar in structure for easier maintenance and reading. So it should be as short, complete and explicit as possible. Modules documentation should be written in reference style, like a man-page. It is not a Tutorial, so it should avoid long examples.

For now, there should be no screen-shots used in the module documentation, since they are not easy to localize and translate. The text should be descriptive enough to be understood without screen shots. In general documentation should be written, to be easy translatable in different languages.

# Template for Module Documentation #
The following template describes the general structure of a documentation page for an individual module. Again, try to not duplicate any existing documentation like `__tryton__.py`, README, INSTALL, LICENSE, COPYRIGHT.

## Module Name ##
  * File or package name

## Short Description ##
  * One paragraph about the general function of the module

## Menu Entries ##
  * Collect and briefly describe all menu entries the module generates.

## Models ##

  * Describe the model without going into too much detail.

### Fields ###
  * Which fields are in the model?
  * Describe function of each Field
  * Don't describe the function of field types (char, one2many, many2many)
    * The functionality and usage of each field type should be described in the general documentation

### Actions ###
  * Describe all actions of the model
  * Don't describe all standard actions of all models like save, delete, new.
    * These are described in the general documentation

## Wizards ##
  * Describe all wizards of the module

## Workflows ##
  * Describe all workflows of the module

## Reports ##
  * File name of the report template

## References ##
  * Links for citation

## External Documentation ##
  * Links to howtos, tutorials, wiki pages, forum entries, bugs or IRC logs.