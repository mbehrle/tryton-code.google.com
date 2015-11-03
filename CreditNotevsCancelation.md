# Credit Note vs. Cancellation Note #

We have to define the terms 'credit note' and 'cancellation note'.

**Note: This is a first research done by the German community based on german law. So perhaps there are differences in other countries. Please contribute.**

For a better understanding we will work with an example. We will talk from "Company1". This is the company that is using Tryton, the explanation is from the point of view of Company1. Party1 is a customer of Company1. Party1 got a delivery of goods from Company1.

The invoice is handled in accounting this way:

## Invoice ##

<table>
<blockquote><tr>
<blockquote><th>Description</th>
<th>Account</th>
<th>Debit</th>
<th>Credit</th>
</blockquote></tr>
<tr>
<blockquote><td>Invoice 1</td>
<td>Main Receivable</td>
<td>1200</td>
<td></td>
</blockquote></tr>
<tr>
<blockquote><td>Invoice 1</td>
<td>Main Revenue</td>
<td></td>
<td>1000</td>
</blockquote></tr>
<tr>
<blockquote><td>Invoice 1</td>
<td>Main Taxes</td>
<td></td>
<td>200</td>
</blockquote></tr>
</table></blockquote>


## Credit Note ##

Lets have a look at 'credit note' first. If we want to understand the handling of a credit note in accounting we need to know what action must happen that a credit note can be written oder needs to be written.

The action behind a credit note is a reverse delivery. This means that Party1 sends back some of the goods. For this delivery Party1 must create an invoice to Company1. But by law it is possible that not Party1 creates an invoice but Company1 creates a credit note for the reverse delivery. There must also be paid attention to the reason of the reverse delivery. The goods must be in original condition for a reverse delivery so that they can be put to stock again by Company1.

This is the only case where a credit note is possible.

So how must this case be handled on accounting?

<table>
<blockquote><tr>
<blockquote><th>Description</th>
<th>Account</th>
<th>Debit</th>
<th>Credit</th>
</blockquote></tr>
<tr>
<blockquote><td>Credit Note 1</td>
<td>Main Receivable</td>
<td></td>
<td>1200</td>
</blockquote></tr>
<tr>
<blockquote><td>Credit Note 1</td>
<td>Main Revenue</td>
<td>1000</td>
<td></td>
</blockquote></tr>
<tr>
<blockquote><td>Credit Note 1</td>
<td>Main Taxes</td>
<td>200</td>
<td></td>
</blockquote></tr>
</table></blockquote>


## Cancellation Note ##

- First example is the cancellation of sold services. For services Party1 cannot do a reverse delivery. For services the amount of an invoice is reduced subsequently. This is one action behind a cancellation note - the subsequent reduction of an invoice.

- Second example is the nullification of a contract. An indicator for a nullification can be the case that all actions are done reverse so that the situation is like before the contract. If there are errors in already opened invoices the cancellation note is the usual way to 'cancel' the invoice so that it can be recreated in the right way again.

- Third action behind a cancellation note is a return in case of a notice of defect. If the goods are sent back because of a notice of defect this is not a reverse delivery but a return. And a return is a case for a cancellation note. The difference is that the goods cannot be put to stock again by Company1 because of the defect.

In accounting a cancellation note is handled like this:

<table>
<blockquote><tr>
<blockquote><th>Description</th>
<th>Account</th>
<th>Debit</th>
<th>Credit</th>
</blockquote></tr>
<tr>
<blockquote><td>Cancellation Note 1</td>
<td>Main Receivable</td>
<td>-1200</td>
<td></td>
</blockquote></tr>
<tr>
<blockquote><td>Cancellation Note 1</td>
<td>Main Revenue</td>
<td></td>
<td>-1000</td>
</blockquote></tr>
<tr>
<blockquote><td>Cancellation Note 1</td>
<td>Main Taxes</td>
<td></td>
<td>-200</td>
</blockquote></tr>
</table>