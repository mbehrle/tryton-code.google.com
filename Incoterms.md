

# Introduction #

This blueprint describes the implementation of trade terms in its current version (trade terms 2010, see https://en.wikipedia.org/wiki/Incoterms ).

Trade terms describe under which conditions goods are delivered/purchased, and by this are part of a sales or purchase contract. The feature request for incoterms was already discussed in https://groups.google.com/d/msg/tryton/qXZQ0nzHC2w/vQB6Q2nTcZ0J

A series of three-letter trade terms related to common contractual sales practices, the Incoterms rules are intended primarily to clearly communicate the tasks, costs, and risks associated with the transportation and delivery of goods [https://en.wikipedia.org/wiki/Incoterms ] .

# Details #

The description of the incoterms 2010 are available from https://en.wikipedia.org/wiki/Incoterms as well.
Incoterms consist of three parts:
  1. The three letter abbreviation (TLA), e.g. FOB
  1. The description of the TLA, e.g. Free on Board
  1. The named destination or port of destination, e.g. Hamburg

In other words, the terms <br>
FOB Hamburg , or <br>
FOB  - Free on Board  Hamburg <br>
describe clearly the obligations and risks for seller and buyer.<br>
<br>
Note that only the description (Free on board) may be subject for translation!<br>
<br>
<blockquote><h2>System usage – Master Data</h2></blockquote>

In most cases one supplier / customer has defined shipment condition. For this reason, it should be possible to include the incoterm in<br>
<ul><li>Customer master<br>
</li><li>Vendor master<br>
</li><li>Material master.<br>
(In case Incoterms are set in material and customer/vendor master, the entry in customer/vendor master should be leading when a sales/purchasing document is created).</li></ul>

<h2>System usage – Transactional Data</h2>
Incoterms are part of the sales resp. purchasing process. Incoterms are set <b>manually</b> along the process, and can be changed during the process (e.g a sale was offered FOB, but the customer decides to buy CIF)<br>
<br>
Incoterms need to be copied along the process chain:<br>
<ul><li>Sales Lead/opportunity, sales order, delivery note, dispatch advice, bill of lading, pro-forma-invoice, invoice.<br>
</li><li>RFQ, purchase order</li></ul>

In case of the invoice, international trade has the speciality that nearly all customs authorities world-wide want to see the 'border-crossing value'. So an invoice may need to have two incoterms:<br>
<ul><li>the incoterm inside the country with the cross-border value (e.g. FCA Brussels 1000 EUR)<br>
</li><li>the incoterm for final destination (e.g. CIF New York 1300 EUR)</li></ul>

<h2>Implementation</h2>
Incoterms should be implemented as customizing table, language dependent, to allow easy changes due to changes in incoterms.<br>
<br>
In the relevant documents it should have a drop-down to select a TLA from the table, fill automatically the description, and have a field (CHAR 40) for destination/origin.