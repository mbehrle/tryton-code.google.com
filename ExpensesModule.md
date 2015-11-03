# Expense Module #

This document will explain the proposed expense module.

Module Name: expense


# Expense #

An expense request is created by an employee.
This expense request will describe what should be bought by the company:

  * Employee
  * Quantity
  * Units
  * Unit Price
  * Currency
  * Expense Type
  * Description
  * Supplier (optional)
  * Date
  * Invoice Line
  * Invoice State
  * State ('draft', 'waiting', 'approved', 'processing', 'done', 'rejected')

The expense will have a specific workflow attached to it to manage its process.

Once the expense object has been confirmed, the expenses will create a supplier invoices grouped per employee/supplier, currency to generate the needed accounting moves.
The expense will have a similar history as the opportunities.
Only user from an expense admin group can approve expenses and they can not approve their own expenses.