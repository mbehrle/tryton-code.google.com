# Introduction #

This document outlines a proposal to improve Tryton production with processes description and operations information.


# Rationale #

Current production module in Tryton is centered around materials. That is, in a production certain products "disappear" (are consumed) and others "appear" (are produced). They are linked together in a production document which is useful for traceability and allows ensuring the costs on the output equal the ones in the input.

Moving one step further should involve:

  * Being able to describe the whole production process including:
    * The instructions needed to fulfill the production
    * The machines and time needed
    * The employees (or Category of Employees) and time needed


Things which are not necessary to address right now but need to be kept in mind include:

  * Being able to add the costs resulting from usage of machines and employees to be added to the cost of the products produced.
  * The definition of the resources to be used should allow proper resource planning in the future (just like current BOM allows planning for stock right now) with an external or integrated planner
  * We should be able to add a means to record employees and machine times. Maybe with start and end timestamps.

# Approaches #

A first approach tried to describe resources based on a Route concept. It was added to production\_route module (http://codereview.tryton.org/4411002) after some discussions about the possibility of documenting the production process **without** having to add the real time and costs in the production.

In order to define the resources (machine and employees) we found that the only relevant measure is time. After all, the production will be able to store how many units of product are consumed and for how long are the resources used. So master models include costs per time unit:

This includes WorkCenter and WorkCenterCategory:

http://codereview.tryton.org/4411002/diff/20001/route.py

A WorkCenter is meant to be a machine or employee whearas WorkCenterCategory is intended to group interchangeable work centers. For example, a work center could be "Alex" and its work center category "Welder". Afterwards, WorkCenter and WorkCenterCategory has been split into Asset and Employee.

Here's a draft of the relations as discussed https://groups.google.com/d/topic/tryton-dev/U9e1Zzjb1n8/discussion:

```
    class BOM:
        operations = fields.One2Many() 


    class OperationType:
        description = fields.Text() 


    class OperationTemplate:
        bom = fields.Many2One() 
        sequence = fields.Integer()
        operation_type = fields.Many2One() # Optional
        description = fields.Text() 
        time = fields.Float() 
        operator = fields.Selection(['linear', 'constant']) 
        asset_resources = fields.One2Many() 
        employee_resources = fields.One2Many() 


    class AssetResource: 
        product = fields.Many2One() 


    class EmployeResource: 
        group = fields.Many2One() 


    class Production: 
        operations = fields.One2Many() 


    class Operation: 
        production = fields.Many2One() 
        sequence = fields.Integer() 
        description = fields.Text() 
        time = fields.Float() 
        assets = fields.One2Many() 
        employees = fields.One2Many() 
        operation_type = fields.Many2One() # Optional


    class OperationAsset: 
        product = fields.Many2One() 
        lot = fields.Many2One()  #  Optional 


    class OperationEmployee: 
        group = fields.Many2One() 
        employee = fields.Many2One()  # Optional 
```



### The Route model ###

The route model would in theory include the steps and resources used to carry  on a production (we'll see in the Processes approach that it is not good enough). So a Route includes a sorted list of operations (Operation) each of which includes a Work Center Category and an OperationType. Given that we're trying to model how much time the given resource is used we must be able to define whether that resource will be used for a fixed amount of time no matter how large the production is (that is, cleaning a machine will always take the same amount of time) or the time depends on the production size.

This behaviour is manged by the `operator` field of type `Selection`.


## Processes ##

Although the Route model correctly allows to model the amount and cost of resources that would be consumed in a production, it is unable of creating a report that fully explains the person that is going to execute the production what steps must be done. The person would know the products needed and would also know what resources are needed but wouldn't have a clue what to do with each of them. Describing that in a separate document (either notes or attached document) is possible but it is far from ideal because it means there will be duplicate information. So the process approach tries to mix existing BOM and the Route concepts into a single structure.

This way, instead of having a BOM and a Route we would have a "Production Process Description" that has a list of steps. Each step would include a list of products to be consumed, list of products that can be produced (output) and the resources used for that step. Also, a text field would tell the user what to do. For example "Mix products to be consumed".

Note that it is more than probable that several steps will have no output because we're just adding products to a mixture and stirring. Others may have wastage as output, for example.

By now, the production\_operation module will not manage those process phases, but it will be easy to extend to implement that from within the BOM.