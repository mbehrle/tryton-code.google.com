# Introduction #

Find here commented listings extracted from module party to explain the use of different elements of views and actions (thx to udono).


# Definition of a standard list view (flat, two dimensional table) #

party/party.xml

```
 
    20         <record model="ir.ui.view" id="party_view_tree">
    21             <field name="model">party.party</field>
    22             <field name="type">tree</field>
    23             <field name="arch" type="xml">
    24                 <![CDATA[
    25                 <tree string="Parties">
    26                     <field name="code" select="1"/>
    27                     <field name="name" select="1"/>
    28                     <field name="lang" select="2"/>
    29                     <field name="vat_code" select="1"/>
    30                 </tree>
    31                 ]]>
    32             </field>
    33         </record>
...
# This is the window action for the list
    89         <record model="ir.action.act_window" id="act_party_form">
    90             <field name="name">Parties</field>
    91             <field name="res_model">party.party</field>
# Here you say form, when you want a flat table
    92             <field name="view_type">form</field>
    93         </record>
# This is the window view action for the list:
    94         <record model="ir.action.act_window.view" id="act_party_form_view1">
# The sequence is used when you press the Change View button. The view cycles throu all available window view actions.
    95             <field name="sequence" eval="10"/>
    96             <field name="view" ref="party_view_tree"/>
    97             <field name="act_window" ref="act_party_form"/>
    98         </record>
# Here is the menu caller which calls the window action above
   104         <menuitem parent="menu_party" sequence="1"
   105             action="act_party_form" id="menu_party_form"/>

```

# Definition of a tree view as a nested table, directed graph #

party/categories.xml

```
    22         <record model="ir.ui.view" id="category_view_tree">
    23             <field name="model">party.category</field>
# same type as a list
    24             <field name="type">tree</field>
# but with a child field, which indicates the different representation
    25             <field name="field_childs">childs</field>
    26             <field name="arch" type="xml">
    27                 <![CDATA[
    28                 <tree string="Categories" fill="1">
    29                     <field name="name" select="1"/>
    30                 </tree>
    31                 ]]>
    32             </field>
    33         </record>

# This is the window action for the nested tree:
    34         <record model="ir.action.act_window" id="act_category_tree">
    35             <field name="name">Categories</field>
    36             <field name="res_model">party.category</field>
# Here you say tree, when you want a tree:
    37             <field name="view_type">tree</field>
# Here you set a domain, to have all branches and leaves nested (not extracted, opened):
    38             <field name="domain">[('parent', '=', False)]</field>
    39         </record>
    40         <record model="ir.action.act_window.view" id="act_category_tree_view1">
    41             <field name="sequence" eval="10"/>
    42             <field name="view" ref="category_view_tree"/>
    43             <field name="act_window" ref="act_category_tree"/>
    44         </record>
    45         <menuitem parent="menu_party"
    46             action="act_category_tree" id="menu_category_tree"/>
```