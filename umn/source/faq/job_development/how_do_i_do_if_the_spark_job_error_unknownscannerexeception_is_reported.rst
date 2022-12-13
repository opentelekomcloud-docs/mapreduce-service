:original_name: mrs_03_1257.html

.. _mrs_03_1257:

How Do I Do If the Spark Job Error "UnknownScannerExeception" Is Reported?
==========================================================================

Symptom
-------

Spark jobs run slowly. Warning information is printed in run logs, and the error cause is **UnknownScannerExeception**.

Solution
--------

Before running a Spark job, adjust the value of **hbase.client.scanner.timeout.period** (for example, from 60 seconds to 120 seconds).

Log in to FusionInsight Manager and choose **Cluster** > **Services** > **HBase**. Click **Configurations** then **All Configurations**, search for **hbase.client.scanner.timeout.period**, and change its value to **120000** (unit: ms).
