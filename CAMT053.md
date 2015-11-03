

# Introduction #

The CAMT.053 Bank to Customer Statement message is used to inform an account
owner or authorized party of entries booked to the account, and to provide
balance information. It may contain reports for more than one account and may
contain statements for more than one book day. It contains information on
booked entries only.

# Small Analysis of the norm #

  * CAMT.053 Group Header
    * Inexistant concept in Tryton
    * Contains the 'CreDtTm' which is the creation datetime of the message
    * Contains the 'MsgId' which uniquely identify the message
    * Contains additional information like the message recipient, message pagination, etc.

  * Statement Header (`account.statement`)
    * We have a `date` / CAMT.053 defines 'CreDtTm' which is the creation datetime
    * 'Id' uniquely identify the statement
    * 'Acct' defines the account on which the entries are made
      * 'Id' contains either 'IBAN' or 'Othr' to identify the account
      * 'Ccy' (currency), 'Nm' (name), 'Ownr' (Owner) are not required fields
    * 'Bal' contains a balance ; CAMT.053 defines 8 types of balances:
      * 'Tp' == `OPBD`: Opening Booked correspond to our `start_balance`
      * 'Tp' == `CLBD`: Closing Booked correspond to our `end_balance`
      * 'Amt' is the amount an attribute Ccy defines the currency used
      * 'Dt' contains either a date 'Dt' or datetime 'DtTm' tag
    * 'TtlNtries' specifies the total number and sum of credit / debit entries
      * 'NbOfNtries' number of lines
      * 'Sum' total of entries
      * 'TtlNetNtryAmt' resulting amount of the netted entries
      * 'CdtDbtInd' credit (`CRDT`) / debit (`DBIT`) indicator
    * Contains additional information like 'FrToDt' (from-to datetime), 'ElctrncSeqNb' (electronic sequence number), 'LglSeqNb' (legal sequence number), etc

  * Statement Lines (`account.statement.line`)
    * 'Amt' The absolute value of the amount ; the Ccy attribute determines the currency
    * 'CdtDbtInd' The credit / debit indicator
    * 'Sts' The status of the entry:
      * `BOOK` Booked: the transfer of money has been completed
      * `INFO` Information: No booking on the account owner's has been  performed
      * `PDNG` Pending: the booking has not been completed.
    * 'BkTxCd' Elements used to identify the type of underlying transaction
    * 'NtryDtls' a non mandatory field providing additional information
      * It can provides information on batched transactions in 'Btch'
      * It can provides inforamtion on the transaction in 'TxDtls'
        * Such information are 'Refs' (reference), 'RltdPties' (related parties), etc.
    * 'BookgDt' a non mandatory field providing the booking date
    * 'ValDt' a non mandatory field providing the value date
    * Additional fields: 'NtryRef' (entry reference), 'RvslInd' (reversal indicator), etc.

# Implementation #

The implementation will follow the implementation of CAMT.054 already present
in `account_payment_sepa`.

In order to handle the missing informations from the statement lines (`account`
and `date`) we will use the non mandatory fields to find the best match for
those fields. In case of doubt the wizard used to process the message will ask
the user to decide the values of the field. It is possible that the user will
process the message by chunks, so a mechanism is added to remember the choice
made previously by the user. Other interesting information (party and invoice),
should also be remembered.

An open question is whether only the entries with 'Sts' == `BOOK` should be
considered for the inclusion in an `account.statement`. Maybe the lines should
have another field to denote their status.

An open question is how to handle the verification method used by
`account.statement`. The fields that would allow to fill the required fields
are not mandatory in CAMT053, so it's not possible to be sure they will be
there. Moreover even if the fields are there, how should entries where 'Sts' is
different then `BOOK` be handled?

## account.statement.sepa.message ##
  * message: `Text`
  * company: `Many2One` to `company.company`
  * state: `Selection`: 'draft', 'processing', 'done', 'cancel'

## account.statement.sepa.message.line ##
  * message: `Many2One` to `account.statement.sepa.message`
  * statement\_id: `Char`
  * line\_index: `Integer`
  * date: `Date`
  * account: `Many2One` to `account.account`
  * invoice: `Many2One` to `account.invoice`
  * party: `Many2One` to `party.party`

## account.statement ##
  * message: `Many2One` to `account.statement.sepa.message`

## account.statement.journal ##
  * sepa\_bank\_account\_number: `Many2One` to `bank.account.number`

# Links #
  * CAMT053 XSD: http://www.iso20022.org/message_archive.page#Bank2CustomerCashManagement
  * CAMT053 guideline from Nederlandse Vereniging van Banken: http://www.betaalvereniging.nl/wp-uploads/2013/11/IG-Bank-to-Customer-Statement-CAMT-053-v1-1.pdf