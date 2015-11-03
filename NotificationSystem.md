# Introduction #

This document outlines a proposal to add a notification system to Tryton
objects.

# Rationale #

Currently there is no way to warn users when specific events occur on object he
is interested in.  In consequence people often misuse the tab-domain feature to
add filters to find the objects in a specific state in some sort of a pull
strategy.

We do think that using a push strategy where a user subscribed to a record (or a
type of records) is warned by the system when specific events occur.

The people customizing the ERP would define a set of interesting events and a
text template to be used when this event happen.  When the event occurs, the
system sends an email (they are not revolutionnized yet!) to every user
subscribed to the record that generated the event.

# Implemenation idea #

According to us, we can reuse the [triggers](TriggerIntegration.md) in order to define the
condition that are met by an interesting event.

Thanks to this idea we can design an Event model that would be something like this
```
class Event:
    trigger = fields.Many2One('ir.trigger', 'Trigger')
    template = fields.Text('Template')
```

The template property is the text that will be transmitted using the transport
protocol ; using some templating engine like genshi is probably a good idea.

In order to be notification-aware a class have to inherit from a specific
`NotificationMixin`. This mixin defines the set of method that will be used in order
to compute the related template and to send the message to the concerned users.

# Open question #

It's still not clear how the `Event` object related to the trigger will be able
to transmit the template information to the `NotificationMixin`.