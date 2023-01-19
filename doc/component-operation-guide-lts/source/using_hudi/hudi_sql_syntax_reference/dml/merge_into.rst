:original_name: mrs_01_24274.html

.. _mrs_01_24274:

MERGE INTO
==========

Function
--------

This command is used to query another table based on the join condition of a table or subquery. If **UPDATE** or **DELETE** is executed for the table matching the join condition, and **INSERT** is executed if the join condition is not met. This command completes the synchronization requiring only one full table scan, delivering higher efficiency than **INSERT** plus **UPDATE**.

Syntax
------

**MERGE INTO** *tableIdentifier* *AS* *target_alias*

**USING** *(sub_query \| tableIdentifier) AS source_alias*

**ON** *<merge_condition>*

*[ WHEN MATCHED [ AND <condition> ] THEN <matched_action> ]*

*[ WHEN MATCHED [ AND <condition> ] THEN <matched_action> ]*

*[ WHEN NOT MATCHED [ AND <condition> ] THEN <not_matched_action> ]*

*<merge_condition> =A equal bool condition*

*<matched_action> =*

*DELETE \|*

``UPDATE SET * |``

*UPDATE SET column1 = expression1 [, column2 = expression2 ...]*

*<not_matched_action> =*

``INSERT * |``

*INSERT (column1 [, column2 ...]) VALUES (value1 [, value2 ...])*

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +--------------------+---------------------------------------------------------------------------------+
   | Parameter          | Description                                                                     |
   +====================+=================================================================================+
   | tableIdentifier    | Name of the Hudi table.                                                         |
   +--------------------+---------------------------------------------------------------------------------+
   | target_alias       | Alias of the target table.                                                      |
   +--------------------+---------------------------------------------------------------------------------+
   | sub_query          | Subquery.                                                                       |
   +--------------------+---------------------------------------------------------------------------------+
   | source_alias       | Alias of the source table or source expression.                                 |
   +--------------------+---------------------------------------------------------------------------------+
   | merge_condition    | Condition for associating the source table or expression with the target table. |
   +--------------------+---------------------------------------------------------------------------------+
   | condition          | Filtering condition. This parameter is optional.                                |
   +--------------------+---------------------------------------------------------------------------------+
   | matched_action     | DELETE or UPDATE operation to be performed when conditions are met.             |
   +--------------------+---------------------------------------------------------------------------------+
   | not_matched_action | INSERT operation to be performed when conditions are not met.                   |
   +--------------------+---------------------------------------------------------------------------------+

Precautions
-----------

#. The merge-on condition supports only primary key columns currently.

#. Currently, only some fields in COW tables can be updated. The following is an example:

   .. code-block::

      merge into h0 using s0
      on h0.id = s0.id
      when matched then update set price = s0.price * 2

#. Currently, only when COW tables are updated, fields in the target table can appear in the right of the UPDATE expression. The following is an example:

   .. code-block::

      merge into h0 using s0
      on h0.id = s0.id
      when matched then update set id = s0.id,
      name = h0.name,
      price = s0.price + h0.price

Examples
--------

.. code-block::

   merge into h0 as target
   using (
   select id, name, price, flag from s
   ) source
   on target.id = source.id
   when matched then update set *
   when not matched then insert *;

   merge into h0
   using (
   select id, name, price, flag from s
   ) source
   on h0.id = source.id
   when matched and flag != 'delete' then update set id = source.id, name = source.name, price = source.price * 2
   when matched and flag = 'delete' then delete
   when not matched then insert (id,name,price) values(source.id, source.name, source.price);

   merge into t0 as target
   using s0 source
   on target.id = source.id
   when matched then update set *
   when not matched then insert *;

System Response
---------------

You can view the result in driver logs or on the client.
