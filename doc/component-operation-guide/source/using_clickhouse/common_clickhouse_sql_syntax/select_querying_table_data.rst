:original_name: mrs_01_24203.html

.. _mrs_01_24203:

SELECT: Querying Table Data
===========================

This section describes the basic syntax and usage of the SQL statement for querying table data in ClickHouse.

Basic Syntax
------------

**SELECT** [**DISTINCT**] expr_list

[**FROM** [*database_name*.]\ *table* \| (subquery) \| table_function] [**FINAL**]

[SAMPLE sample_coeff]

[ARRAY **JOIN** ...]

[**GLOBAL**] [**ANY**\ \|\ **ALL**\ \|\ **ASOF**] [**INNER**\ \|\ **LEFT**\ \|\ **RIGHT**\ \|\ **FULL**\ \|\ **CROSS**] [**OUTER**\ \|SEMI|ANTI] **JOIN** (subquery)\|\ **table** (**ON** <expr_list>)|(**USING** <column_list>)

[PREWHERE expr]

[**WHERE** expr]

[**GROUP BY** expr_list] [**WITH** TOTALS]

[**HAVING** expr]

[**ORDER BY** expr_list] [**WITH** FILL] [**FROM** expr] [**TO** expr] [STEP expr]

[**LIMIT** [offset_value, ]n **BY** columns]

[**LIMIT** [n, ]m] [**WITH** TIES]

[**UNION ALL** ...]

[**INTO** OUTFILE filename]

[FORMAT format]

Example
-------

.. code-block::

   -- View ClickHouse cluster information.
   select * from system.clusters;
   -- View the macros set for the current node.
   select * from system.macros;
   -- Check the database capacity.
   select
   sum(rows) as "Total number of rows",
   formatReadableSize(sum(data_uncompressed_bytes)) as "Original size",
   formatReadableSize(sum(data_compressed_bytes)) as "Compression size",
   round(sum(data_compressed_bytes) / sum(data_uncompressed_bytes) * 100,
   0) "Compression rate"
   from system.parts;
   -- Query the capacity of the test table. Add or modify the where clause based on the site requirements.
   select
   sum(rows) as "Total number of rows",
   formatReadableSize(sum(data_uncompressed_bytes)) as "Original size",
   formatReadableSize(sum(data_compressed_bytes)) as "Compression size",
   round(sum(data_compressed_bytes) / sum(data_uncompressed_bytes) * 100,
   0) "Compression rate"
   from system.parts
   where table in ('test')
   and partition like '2020-11-%'
   group by table;
