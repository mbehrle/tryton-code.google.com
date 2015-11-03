**Implemented**: [account\_asset](http://hg.tryton.org/modules/account_asset)

# Account Assets Management #

This document will explain the proposed account assets module.

Module Name: account\_assets
dep
# Assets #

The assets document will describe how the assets will be depreciated, it will contain:

  * Product (type assets)
  * Supplier invoice line
  * Account Journal
  * Quantity (filled from invoice line)
  * Value (filled from invoice line)
  * Residual Value
  * Depreciation Amount
  * Start Date (is it always the date of the incoming moves?)
  * End Date
  * Depreciation method:
    * linear
  * Frequency: ('monthly', 'yearly')
  * State: ('draft', 'running', 'done', 'cancel')
  * Lines:
    * Date
    * Amount
    * Move (link to the account move)
    * Value depreciated
    * Accumulate depreciation

## Workflow ##

When the assets will be validated, the lines will be generated for each period. (Generation could be also done on demand in 'draft' state.)
A wizard on assets will create the accounting move for all lines before a date.
When a running assets will be reset to draft, all the lines without accounting move will be deleted. And when validated, the assets value used to computed the remaining lines will be reduced by the amount already depreciated.

# Product #

The product will be extended to contain:

  * account depreciation

# Selling Assets #

The Sale Line and Invoice Line will be extended to contain:

  * assets (when product is asset)

## Workflow ##

When validating the invoice, the assets depreciation will be balanced with the account revenue. The quantity of assets will be decrease by the invoiced quantity and the lines in the futures will be recomputed.