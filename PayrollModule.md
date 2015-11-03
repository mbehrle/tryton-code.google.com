

# Introduction #

This is a description about what a general payroll process is. Taking in account some special features present many companies.

# Objetives #
  * Implement a general payroll module.
  * Give a kind freedom to customize some process and special cases.
  * Print basic reports.

# Process Description #

## Basic Payroll Process ##
![http://www.opdevel.com/tryton/images/Payroll_WF.jpg](http://www.opdevel.com/tryton/images/Payroll_WF.jpg)

This diagram describes as general as possible the payroll process, starting from employee creation that will be an extention of party module to manage some features related to human resources including contract management and all types of wages classified in three main categories like **payments** (e.g: Salary), **discounts** (e.g: Bank Credits), **deductions** (e.g: Social Security) and finally followed by the Payroll Liquidation specified in the next diagram.

## Payroll Liquidation Process ##

![http://www.opdevel.com/tryton/images/Payroll_Liquidation_WF.jpg](http://www.opdevel.com/tryton/images/Payroll_Liquidation_WF.jpg)

This workflow explains a generic Payroll Liquidation taking in account when a contract expires, when an employee gets in holidays and finalize with a pre-liquidation where is possible to add new concepts (e.g: Permissions, Bonuses) and finalize the process.

## Initial Design ##

This diagram is an initial idea integrating some existing modules in Tryton.

![http://www.opdevel.com/tryton/images/Payroll_trytonDC.jpg](http://www.opdevel.com/tryton/images/Payroll_trytonDC.jpg)

**Note:** Here is not contempled anything related with reports needed.

# Main Features #

  * Contract Management.
  * Special Cases definition.
  * Wage Types Management.
    * Payments
    * Deductions
    * Discounts
  * Holidays Management.
  * Salary History
  * Contract History

# References #

  * A short [Payroll](http://en.wikipedia.org/wiki/Payroll) description.
  * [Employee Benefits](http://www.iasplus.com/standard/ias19.htm)