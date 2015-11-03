#summary Collect your knowledge about tryton module development
#labels Deprecated,Phase-Implementation
# Model/Class/Object #
## Model inside ##
### Q: What is the meaning of _rec\_name entrys in a model? ###_

A: It's used when there is no "name" field on an object, if you don't have a field named 'name' you choose with _rec\_name an alias. The field in_rec\_name will be used to display many2one field for example.


# View's #
For the exact description of the different view types, please refer to the appropriate DTD.

## Graph ##
please refer to [trytond/trytond/ir/ui/graph.dtd](http://www.tryton.org/hg/trytond/file/tip/trytond/ir/ui/graph.dtd)

### How to edit a graph view ###
  * Admin menu > ir > ui > views
  * Select the appropriate view
  * Show: trytond/ir/ui/graph.dtd for the possibilities

## Form ##
please refer to [trytond/trytond/ir/ui/form.dtd](http://www.tryton.org/hg/trytond/file/tip/trytond/ir/ui/form.dtd)

field
label

## Propertys ##
colspan="4"

col="6"

align="0.0"

fill="1"

xexpand="1"

expand="1"

select="1"

select="2"

tree\_invisible="1"

eval="8"

widget="float\_time" sum="Hours"

width="300"

search="[('name', '=', 'company'), ('model.model', '=', 'stock.move')]"

ref="act\_move\_form\_cust"

invisible="1"

width="600"

height="400"