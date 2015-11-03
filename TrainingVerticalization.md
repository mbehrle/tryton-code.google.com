

# Introduction #

This document will explain the proposed modules to manage training activities based on courses. All functionalities will be supplied by several modules.

# Rationale: Objectives and Features #

These modules should allow to manage training activities from different prespectives (which are not independant):

  * resource management: available seats?, calendar, rooms, teachers...
  * course monitoring (specially for long term courses): progress status, assistance...
  * student monitoring: assistance, evaluation, courses history (student record)...
  * sale/subscription process
  * teachers allocation/subcontracting

The first three points are common in all use case, but the last two depends of the use case.

Focusing in the sale/subscription process, I dentify three use cases:

  * **internal training**: to manage internal training of the employees or members of organization.
    * very simple subscription process
    * control of seats availability
    * **without sale nor invoice** => no related product needed
  * **seats sold individually**: The company offers courses and individuals enroll it. Served _from stock_
    * subcription process and control of seats availability
    * invoice generation based on subscriptions => required product related to course (price by seat)
    * optionally, the subscription could be generated from a sale, where each line corresponds to a subscription
  * **courses sold as package**: The company offers courses to organizations for be _consumed_ by its employees, members... Serverd _on demand_.
    * very simple subscription process
    * The course is related to a sale line. Required product related to course. **Price by seat** (the quantity of sale line is the number of seats sold (the course's max available seats) or **Price by course** (quantity is 1).
    * Two invoice methods: _On Order Processed_ (the invoice is independent of number of subscriptions) or _On Subscription Done_ (equivalent to _On Shipment Sent_) where the number of subscriptions is used to compute the invoice amount.

Focusing in the teachers allocation/subcontracting:
  * **internal teachers**: teachers doesn't have a payment based on done sessions. Provable they are employees.
    * very simple allocation process. Process not managed in the ERP, the manager set the selected teacher. Some helps as session's calendar view by course and by teacher
    * optional, it generates timesheet entries to manage analytic costs
  * **external teachers**: teachers are subcontracted and paid based on done sessions
    * very simple allocation process. Idem.
    * invoice generation based on sessions done => required product related to course or teacher. **price by hour** or **price by session**
    * generate invoice periodically (all sessions done in a month) or by course
    * optional, the allocation is preceded by a purchase process where a session is _offered/requested_ to some teachers who could accept or not.


# Details #

## Modules ##

  * **trainig**: defines the entities of _course_, _session_, course and session basic categorization, course and session templates, teacher and students (party extension). Implement the use cases **internal training** and **internal teachers** (without dependencies with account, sale nor purchase)
  * **training\_invoice**: implement the use case **seats sold individually** related to customer invoices, and the basic **external teachers** related to supplier (it could be separated in two modules: _training\_customer_ and _training\_supplier_ but I think it's better less module and in the Configuration could activate or deactivate the customer/supplier invoicing by each company.
  * **training\_sale**: implement the use case **courses sold as package** and extends the use case **seats sold individually** with subscription generation from sale.
  * **training\_purchase**: extend the allocation process in use case **external teachers** with the purchase requests generation.

## Training module ##

  * **training.format**: f.e: in-person, on-line, intensive.
    * name
    * min\_seats, max\_seats: limit of seats. It will be used in on\_change in training.course and when create courses from templates
  * **training.course.category**: to organize your courses.
    * parent/childs: hierarchical organization
    * name
    * description: text
  * **training.template.course** (maybe it could be training.offer, and next
> > training.offer.session)
    * name (required)
    * category (M2O training.course.category, required)
    * format (M2O training.format, optional)
    * force\_format (boolean, visible/editable only if format is not empty): force that all sessions of course have the course's format
    * language (optional)
    * force\_language (boolean, visible/editable only if language is not empty): force that all sessions of course have the course's language
    * sessions (O2M training.template.session, or M2M with 'sequence' in M2M class and allow to select/add sessions as M2M fields)
    * goal, descrition, requirements (Text, optional)
  * **training.template.session**
    * course (M2O training.template.course, required)
    * sequence (integer, required)
    * name (required)
    * format (M2O training.format, required)
    * duration (float, in hours, required)
    * language (optional, invisible if course.force\_format))
    * available\_teachers (M2M party.party teacher=True, optional)
  * **training.course**
    * all the fields of training.template.course
    * template (M2O training.template.course, optional)
    * code (filled by sequence)
    * start\_date (datetime, required)
    * end\_date (functional datetime)
    * address (M2O party.address, required)
    * min\_seats, max\_seats (integer, required, take from format if set)
    * manager (M2O res.user)
    * sessions (O2M tratining.session)
    * subscriptions (O2M training.subscription, readonly)
    * total\_duration, n\_sessions (functional fields based on sessions data)
    * n\_subscriptions, available\_seats (functional fields based on subscriptions data)
    * state: draft, confirmed, in progress, done, cancelled
  * **training.session**
    * all the fields of training.template.session
    * template (M2O training.template.session, optional)
    * course (M2O training.course, required)
    * date (datetime, required)
    * teacher (M2M party.party teacher=True, if template and template.teachers, domain teacher in template.teachers)
    * participations (O2M training.session.participation)
    * state: draft, confirmed, done, attendance\_reported, cancelled)
  * **training.subscription**
    * student (M2O party.party, required)
    * course (M2O training.course, required)
    * code (filled by sequence)
    * date (date, required)
    * note (text)
    * origin (reference)
    * assistance (functional float with % of assistance)
    * passed (selection: pending, retake sessions, no passed, passed)
    * state (draft, confirmed, done, evaluated, cancelled): done is set automatically when the course is done
    * confirmation\_date (date)
    * cancellation\_date (date)
  * **training.session.participation** (M2M class of session

&lt;-&gt;

subscription)
    * session (M2O training.session)
    * subscription (M2O training.subscription)
    * attended (boolean)
  * **training.configuration**:
    * session\_format (M2O training.format, required): used as default value for _training.session_ (not in templates?)
    * course\_sequence (Property/Functional company dependant M2O ir.sequence, required)
    * subscripton\_sequence(Property/Functional company dependantM2O ir.sequence, required)

## Training Invoice module ##

TODO: I'm working on it

## Training Sale module ##

I don't need it for now.

## Training Purchase module ##

I don't need it for now.