:original_name: mrs_01_1471.html

.. _mrs_01_1471:

Why the UPDATE Command Cannot Be Executed in Spark Shell?
=========================================================

Question
--------

Why the UPDATE command cannot be executed in Spark Shell?

Answer
------

The syntax and examples provided in this document are about Beeline commands instead of Spark Shell commands.

To run the UPDATE command in Spark Shell, use the following syntax:

-  Syntax 1

   **<carbon_context>.sql("UPDATE <CARBON TABLE> SET (column_name1, column_name2, ... column_name n) = (column1_expression , column2_expression , column3_expression ... column n_expression) [ WHERE { <filter_condition> } ];").show**

-  Syntax 2

   **<carbon_context>.sql("UPDATE <CARBON TABLE> SET (column_name1, column_name2,) = (select sourceColumn1, sourceColumn2 from sourceTable [ WHERE { <filter_condition> } ] ) [ WHERE { <filter_condition> } ];").show**

Example:

If the context of CarbonData is **carbon**, run the following command:

**carbon.sql("update carbonTable1 d set (d.column3,d.column5) = (select s.c33 ,s.c55 from sourceTable1 s where d.column1 = s.c11) where d.column1 = 'country' exists( select \* from table3 o where o.c2 > 1);").show**
