# Introduction #

This document outlines a proposal to add a module allowing to group outgoing shipments.


# Rationale #

Currently each sale order will create one outgoing shipment while sometimes it
is possible to group outgoing moves from different origin on the same shipment.

# Details #

The design of this module should closely follow the design of the
`sale_invoice_grouping` module.

There is a small divergence though on the computation of the domain used to
find the matching shipments. Since we might want to delay some movements by
postposing their planned date a method on the shipment object will allow to
define the clause used for the `planned_date` field.