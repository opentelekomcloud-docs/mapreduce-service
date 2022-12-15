:original_name: mrs_08_00349.html

.. _mrs_08_00349:

Flink CEP in SQL
================


Flink CEP in SQL
----------------

Flink allows users to represent complex event processing (CEP) query results in SQL for pattern matching and evaluate event streams on Flink engines.

SQL Query Syntax
----------------

CEP SQL is implemented through the **MATCH_RECOGNIZE** SQL syntax. The **MATCH_RECOGNIZE** clause is supported by Oracle SQL since Oracle Database 12c and is used to indicate event pattern matching in SQL. Apache Calcite also supports the **MATCH_RECOGNIZE** clause.

Flink uses Calcite to analyze SQL query results. Therefore, this operation complies with the Apache Calcite syntax.

.. code-block::

   MATCH_RECOGNIZE (
         [ PARTITION BY expression [, expression ]* ]
         [ ORDER BY orderItem [, orderItem ]* ]
         [ MEASURES measureColumn [, measureColumn ]* ]
         [ ONE ROW PER MATCH | ALL ROWS PER MATCH ]
         [ AFTER MATCH
               ( SKIP TO NEXT ROW
               | SKIP PAST LAST ROW
               | SKIP TO FIRST variable
               | SKIP TO LAST variable
               | SKIP TO variable )
         ]
         PATTERN ( pattern )
         [ WITHIN intervalLiteral ]
         [ SUBSET subsetItem [, subsetItem ]* ]
         DEFINE variable AS condition [, variable AS condition ]*
         )

The syntax elements of the **MATCH_RECOGNIZE** clause are defined as follows:

(Optional) **-PARTITION BY**: defines partition columns. This clause is optional. If this parameter is not defined, the parallelism 1 is used.

(Optional) **-ORDER BY**: defines the sequence of events in a data flow. The **ORDER BY** clause is optional. If it is ignored, non-deterministic sorting is used. Since the order of events is important in pattern matching, this clause should be specified in most cases.

(Optional) **-MEASURES**: specifies the attribute value of the successfully matched event.

(Optional) **-ONE ROW PER MATCH \| ALL ROWS PER MATCH**: defines how to output the result. **ONE ROW PER MATCH** indicates that only one row is output for each matching. **ALL ROWS PER MATCH** indicates that one row is output for each matching event.

(Optional) **-AFTER MATCH**: specifies the start position for processing after the next pattern is successfully matched.

**-PATTERN**: defines the matching pattern as a regular expression. The following operators can be used in the **PATTERN** clause: join operators, quantifier operators (``*``, +, ?, {n}, {n,}, {n,m}, and {,m}), branch operators (vertical bar \|), and differential operators ('{- -}').

(Optional) **-WITHIN**: outputs a pattern clause match only when the match occurs within the specified time.

(Optional) **-SUBSET**: combines one or more associated variables defined in the **DEFINE** clause.

**-DEFINE**: specifies the Boolean condition, which defines the variables used in the **PATTERN** clause.

In addition, the **MATCH_RECOGNIZE** clause supports the following functions:

**-MATCH_NUMBER()**: Used in the **MEASURES** clause to allocate the same number to each row that is successfully matched.

**-CLASSIFIER()**: Used in the **MEASURES** clause to indicate the mapping between matched rows and variables.

**-FIRST()** and **LAST()**: Used in the **MEASURES** clause to return the value of the expression evaluated in the first or last row of the row set mapped to the schema variable.

**-NEXT()** and **PREV()**: Used in the **DEFINE** clause to evaluate an expression using the previous or next row in a partition.

**-RUNNING** and **FINAL** keywords: Used to determine the semantics required for aggregation. **RUNNING** can be used in the **MEASURES** and **DEFINE** clauses, whereas **FINAL** can be used only in the **MEASURES** clause.

- Aggregate functions (**COUNT**, **SUM**, **AVG**, **MAX**, **MIN**): Used in the **MEASURES** and **DEFINE** clauses.

Query Example
-------------

The following query finds the V-shaped pattern in the stock price data flow.

.. code-block::

   SELECT *
       FROM MyTable
       MATCH_RECOGNIZE (
         ORDER BY rowtime
         MEASURES
           STRT.name as s_name,
           LAST(DOWN.name) as down_name,
           LAST(UP.name) as up_name
         ONE ROW PER MATCH
         PATTERN (STRT DOWN+ UP+)
         DEFINE
           DOWN AS DOWN.v < PREV(DOWN.v),
           UP AS UP.v > PREV(UP.v)
       )

In the following query, the aggregate function **AVG** is used in the **MEASURES** clause of **SUBSET E** consisting of variables related to A and C.

.. code-block::

   SELECT *
       FROM Ticker
       MATCH_RECOGNIZE (
         MEASURES
           AVG(E.price) AS avgPrice
         ONE ROW PER MATCH
         AFTER MATCH SKIP PAST LAST ROW
         PATTERN (A B+ C)
         SUBSET E = (A,C)
         DEFINE
           A AS A.price < 30,
           B AS B.price < 20,
           C AS C.price < 30
       )
