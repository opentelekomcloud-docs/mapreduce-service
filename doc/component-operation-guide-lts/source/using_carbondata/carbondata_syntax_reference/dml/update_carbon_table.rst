:original_name: mrs_01_1439.html

.. _mrs_01_1439:

UPDATE CARBON TABLE
===================

Function
--------

This command is used to update the CarbonData table based on the column expression and optional filtering conditions.

Syntax
------

-  Syntax 1:

   **UPDATE <CARBON TABLE> SET (column_name1, column_name2, ... column_name n) = (column1_expression , column2_expression , column3_expression ... column n_expression ) [ WHERE { <filter_condition> } ];**

-  Syntax 2:

   **UPDATE <CARBON TABLE> SET (column_name1, column_name2,) = (select sourceColumn1, sourceColumn2 from sourceTable [ WHERE { <filter_condition> } ] ) [ WHERE { <filter_condition> } ];**

Parameter Description
---------------------

.. table:: **Table 1** UPDATE parameters

   +--------------+-------------------------------------------------------------------------------+
   | Parameter    | Description                                                                   |
   +==============+===============================================================================+
   | CARBON TABLE | Name of the CarbonData table to be updated                                    |
   +--------------+-------------------------------------------------------------------------------+
   | column_name  | Target column to be updated                                                   |
   +--------------+-------------------------------------------------------------------------------+
   | sourceColumn | Column value of the source table that needs to be updated in the target table |
   +--------------+-------------------------------------------------------------------------------+
   | sourceTable  | Table from which the records are updated to the target table                  |
   +--------------+-------------------------------------------------------------------------------+

Precautions
-----------

Note the following before running this command:

-  The UPDATE command fails if multiple input rows in the source table are matched with a single row in the target table.

-  If the source table generates empty records, the UPDATE operation completes without updating the table.

-  If rows in the source table do not match any existing rows in the target table, the UPDATE operation completes without updating the table.

-  UPDATE is not allowed in the table with secondary index.

-  In a subquery, if the source table and target table are the same, the UPDATE operation fails.

-  The UPDATE operation fails if the subquery used in the UPDATE command contains an aggregate function or a GROUP BY clause.

   For example, **update t_carbn01 a set (a.item_type_code, a.profit) = ( select b.item_type_cd, sum(b.profit) from t_carbn01b b where item_type_cd =2 group by item_type_code);**.

   In the preceding example, aggregate function **sum(b.profit)** and GROUP BY clause are used in the subquery. As a result, the UPDATE operation will fail.

-  If the **carbon.input.segments** property has been set for the queried table, the UPDATE operation fails. To solve this problem, run the following statement before the query:

   Syntax:

   **SET carbon.input.segments. <database_name>. <table_name>=\***;

Examples
--------

-  Example 1:

   **update carbonTable1 d set (d.column3,d.column5 ) = (select s.c33 ,s.c55 from sourceTable1 s where d.column1 = s.c11) where d.column1 = 'country' exists( select \* from table3 o where o.c2 > 1);**

-  Example 2:

   **update carbonTable1 d set (c3) = (select s.c33 from sourceTable1 s where d.column1 = s.c11) where exists( select \* from iud.other o where o.c2 > 1);**

-  Example 3:

   **update carbonTable1 set (c2, c5 ) = (c2 + 1, concat(c5 , "y" ));**

-  Example 4:

   **update carbonTable1 d set (c2, c5 ) = (c2 + 1, "xyx") where d.column1 = 'india';**

-  Example 5:

   **update carbonTable1 d set (c2, c5 ) = (c2 + 1, "xyx") where d.column1 = 'india' and exists( select \* from table3 o where o.column2 > 1);**

System Response
---------------

Success or failure will be recorded in the driver log and on the client.
