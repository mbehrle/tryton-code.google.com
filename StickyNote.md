# Introduction #

This document outlines a proposal to add a sticky note system to Tryton objects.

# Rational #

Currently there are some objects that have a description text field which is used as a sticky note most of the time. But this is a misuse because there is  some important information missing like the author, the date etc.

So the idea is to have a functionality quite similar to the current attachment feature but for simple notes (text).

# Implementation Idea #

A new Model `ir.note` could be created containing just a message field, a resource field and a list of `users` having read the note.
The client could be extended to add an other button next to the attachment one. This button could be highlighted if there are unread notes for the user.
The custom dialog will present a list of ordered notes with a text field on the bottom to post a new message. The list will have a checkbox to mark a note as read.
The list could also display the author and the date.

# Future Improvement #

The dialog box could poll the server to be notified of new messages and then refresh the list on the fly.