:original_name: mrs_01_1952.html

.. _mrs_01_1952:

Configuring the Default Number of Data Blocks Divided by SparkSQL
=================================================================

Scenarios
---------

By default, SparkSQL divides data into 200 data blocks during shuffle. In data-intensive scenarios, each data block may have excessive size. If a single data block of a task is larger than 2 GB, an error similar to the following will be reported while Spark attempts to fetch the data block:

.. code-block::

   Adjusted frame length exceeds 2147483647: 2717729270 - discarded

For example, setting the number of default data blocks to 200 causes SparkSQL to encounter an error in running a TPCDS 500-GB test. To avoid this, increase the number of default blocks in data-intensive scenarios.

Configuration parameters
------------------------

**Navigation path for setting parameters:**

On Manager, choose **Cluster > *Name of the desired cluster* > Service** > **Spark2x** > **Configuration** and click **All Configurations**. Enter a parameter name in the search box.

.. table:: **Table 1** Parameter description

   +------------------------------+----------------------------------------------------------------+---------------+
   | Parameter                    | Description                                                    | Default Value |
   +==============================+================================================================+===============+
   | spark.sql.shuffle.partitions | Indicates the default number of blocks divided during shuffle. | 200           |
   +------------------------------+----------------------------------------------------------------+---------------+
