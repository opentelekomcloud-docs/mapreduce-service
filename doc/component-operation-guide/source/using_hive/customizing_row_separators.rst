:original_name: mrs_01_0955.html

.. _mrs_01_0955:

Customizing Row Separators
==========================

Scenario
--------

In most cases, a carriage return character is used as the row delimiter in Hive tables stored in text files, that is, the carriage return character is used as the terminator of a row during queries. However, some data files are delimited by special characters, and not a carriage return character.

MRS Hive allows you to use different characters or character combinations to delimit rows of Hive text data. When creating a table, set **inputformat** to **SpecifiedDelimiterInputFormat**, and set the following parameter before search each time. Then the table data is queried by the specified delimiter.

**set hive.textinput.record.delimiter='';**

.. note::

   -  The Hue component of the current version does not support the configuration of multiple separators when files are imported to a Hive table.
   -  This section applies to MRS 3.\ *x* or later.

Procedure
---------

#. Specify **inputFormat** and **outputFormat** when creating a table.

   **CREATE [TEMPORARY] [EXTERNAL] TABLE [IF NOT EXISTS]** *[db_name.]table_name* **[(**\ *col_name data_type* **[COMMENT** *col_comment*\ **],** *...*\ **)] [ROW FORMAT** *row_format*\ **] STORED AS inputformat 'org.apache.hadoop.hive.contrib.fileformat.SpecifiedDelimiterInputFormat' outputformat 'org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat'**

#. Specify the delimiter before search.

   **set hive.textinput.record.delimiter='!@!'**

   Hive will use '!@!' as the row delimiter.
