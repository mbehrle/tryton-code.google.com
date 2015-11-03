# Support Ticket System #

The support ticket works closest to the project / timesheet concepts of Tryton.
The models are

## Ticket ##

historised

`_inherits = {'timesheet.work': 'work'}`

name field will be filled with the sequence of ticket

  * work = Many2One - `timesheet.work`
  * title = Char
  * owner = Many2One - `party.party`
  * comment = fields.Function(getter-set empty, setter-set the field)
  * assigned\_to: Many2One `company.employee`
  * follow\_ups: One2Many History (refer History Fields tree below)
  * state = Many2One `ticket.states`
  * last\_updated\_by = Invisible Char field to be filled at Create Write from the context. If GTK client, then fill the User, if by email the context should be appropriately set in the context.

### History Fields (Tree) ###
  * datetime
  * author (Char - Employee/Party/User/email - depending on write mechanism)
  * comment
  * state

### History Fields (Form) ###
  * datetime
  * author
  * title
  * owner
  * comment
  * assigned\_to
  * state


## States ##
`_name = "ticket.states"`
`_order = sequence ASC`

  * name: Char
  * sequence: Integer

## Configuration ##
`_name = "ticket.configuration"`

sequence = property(Many2one(ir.sequence)) (by default sequence with prefix 'ticket' Note:define in XML for the sequence prefix)

## Presentation ##
### Menus ###
  * Support Management
    * Configuration
      * Ticket Settings
      * States
    * Tickets
      * Tickets by State
      * New Ticket

## Future Improvements ##

  * Integration with email system
    * Generate ticket from email
    * Update followups by email