:original_name: mrs_01_2039.html

.. _mrs_01_2039:

Why No Result Is found When 2016-6-30 Is Set in the Date Field as the Filter Condition?
=======================================================================================

Question
--------

Why no result is found when 2016-6-30 is set in the date field as the filter condition?

As shown in the following figure, trx_dte_par in the select count (``*``) from trxfintrx2012 a where trx_dte_par='2016-6-30' statement is a date field. However, no search result is found when the filter condition is where trx_dte_par='2016-6-30'. Search results are found only when the filter condition is where trx_dte_par='2016-06-30'.


.. figure:: /_static/images/en-us_image_0000001348771241.jpg
   :alt: **Figure 1** Example

   **Figure 1** Example

Answer
------

If a data string of the date type is present in Spark SQL statements, the Spark SQL will search the matching character string without checking the date format. In this case, if the date format in the SQL statement is incorrect, the query will fail. For example, if the data format is yyyy-mm-dd, then no search results matching '2016-6-30' will be found.
