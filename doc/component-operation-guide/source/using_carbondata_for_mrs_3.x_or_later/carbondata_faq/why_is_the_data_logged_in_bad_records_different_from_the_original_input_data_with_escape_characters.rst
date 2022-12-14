:original_name: mrs_01_1462.html

.. _mrs_01_1462:

Why Is the Data Logged in Bad Records Different from the Original Input Data with Escape Characters?
====================================================================================================

Question
--------

Why is the data logged in bad records different from the original input data with escaped characters?

Answer
------

An escape character is a backslash (\\) followed by one or more characters. If the input records contain escape characters such as \\t, \\b, \\n, \\r, \\f, \\', \\", \\\\ , java will process the escape character '\\' and the following characters together to obtain the escaped meaning.

For example, if the CSV data type **2010\\\\10,test** is inserted to String,int type, the value is treated as bad records, because **tes**\ t cannot be converted to int. The value logged in the bad records is **2010\\10** because java processes **\\\\** as **\\**.
