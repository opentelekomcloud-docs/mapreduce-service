:original_name: mrs_01_24775.html

.. _mrs_01_24775:

Creating a CDL Data Comparison Job
==================================

Scenario
--------

Data comparison checks the consistency between data in the source database and that in the target Hive. If the data is inconsistent, CDL can attempt to repair the inconsistent data.

The current data comparison task supports manual full comparison. The data comparison task runs in On Yarn mode, and the comparison result is uploaded to HDFS directories.

.. note::

   -  Currently, only basic data types can be compared. Special data types such as date, timestamp, decimal, numeric, and JSON cannot be compared.
   -  Data cannot be compared for tables whose field names contain database keywords.
   -  A data comparison task for a single table supports comparison of a maximum of 100 fields. If a table contains more than 100 fields, you can specify two whitelists of different comparison fields for data comparison.
   -  Currently, only the data captured from PgSQL to Hudi can be compared. If the comparison result is inconsistent, a report address is generated only when there are no more than 2000 inconsistent data records. If there are more than 2000 inconsistent data records, no report address is generated and data cannot be repaired.
   -  If the Kafka lag of the CDL task involved in the comparison is not 0, the comparison result is inconsistent.

Prerequisites
-------------

#. You have prepared the Hive UDF JAR package, copied **${BIGDATA_HOME}/FusionInsight_CDL_*/install/FusionInsight-CDL-*/cdl/hive-checksum/cdl-dc-hive-checksum-*.jar** from the CDL installation directory to the **${BIGDATA_HOME}/third_lib/Hive** directory of Hive, and set the permission on the JAR package to **750** or higher.

#. A user with the CDL management permission has been created for the cluster with Kerberos authentication enabled.. If Ranger authentication is enabled for the current cluster, grant the Hive administrator permission and UDF operation permission to the user by referring to :ref:`Adding a Ranger Access Permission Policy for Hive <mrs_01_1858>`.

#. You have created a global UDF algorithm on the Hive client as a user with the Hive administrator permission.

   Run the following command to create the **CheckSum** function in the default database:

   **create function checksum_aggregate as 'com.xxx.hive.checksum.ChecksumUdaf'**

#. A CDL synchronization task exists. The comparison task determines the data to be compared based on the synchronization task status and data synchronization status.

#. The database user in the data synchronization task associated with data comparison task must have the **create function** permission on the current schema.

Procedure
---------

#. Log in to the CDLService web UI as the created user user (for the cluster where Kerberos authentication is not enabled). For details, see :ref:`Logging In to the CDLService WebUI <mrs_01_24236>`.

#. Choose **Job Management** > **Data comparison task** and click **Add Job**. In the displayed dialog box, set related job parameters and click **Next**.

   +---------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------+
   | Parameter     | Description                                                                                                                                                     | Example      |
   +===============+=================================================================================================================================================================+==============+
   | Name          | Name of the data comparison task.                                                                                                                               | job_dc_test  |
   +---------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------+
   | CDL Job Name  | Name of the associated synchronization task. (Note: The user who runs the comparison task is the user of the Hudi Link in the associated synchronization task.) | pg2hudi_test |
   +---------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------+
   | Execution Env | Environment variable required for running Spark tasks. If no ENV is available, create one by referring to :ref:`Managing ENV <mrs_01_24255>`.                   | dc_env       |
   +---------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------+
   | Desc          | Description of the task.                                                                                                                                        | ``-``        |
   +---------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------+

#. On the **Create Compare-Pair** page, set related parameters and click **Create**.

   +-------------------+------------------------------------------------+-----------+
   | Parameter         | Description                                    | Example   |
   +-------------------+------------------------------------------------+-----------+
   | Name              | Name of the current comparison task.           | test      |
   +-------------------+------------------------------------------------+-----------+
   | Source Table      | Source table name.                             | tabletest |
   +-------------------+------------------------------------------------+-----------+
   | Target Table      | Target table name.                             | tabletest |
   +-------------------+------------------------------------------------+-----------+
   | WhiteList Columns | Column family involved in data comparison.     | ``-``     |
   +-------------------+------------------------------------------------+-----------+
   | BlackList Columns | Column family not involved in data comparison. | ``-``     |
   +-------------------+------------------------------------------------+-----------+
   | Where Condition   | User-defined comparison conditions.            | ``-``     |
   +-------------------+------------------------------------------------+-----------+

   To compare multiple tables, click **Add**.

#. In the data comparison task list, click **Start** in the row of the task to start data comparison.

#. After the execution is complete, view the result in the **Comparing Result** column.

   |image1|

#. If the result is **Inconsistent**, click **More** and select **view records**.

   |image2|

#. In the **Task Run Log** window, locate the target task and click **View Results** in the **Operation** column.

   |image3|

#. Click **Repair** to repair the data.

   |image4|

#. After the repair is complete, check whether the value of **Comparing Result** is **Consistent**. If yes, data repair is successful. If not, the repair fails. In this case, obtain the report from the corresponding HDFS directory based on the value of **Report Path** and manually repair the data.

   |image5|

.. |image1| image:: /_static/images/en-us_image_0000001583391853.png
.. |image2| image:: /_static/images/en-us_image_0000001583272157.png
.. |image3| image:: /_static/images/en-us_image_0000001582952089.png
.. |image4| image:: /_static/images/en-us_image_0000001532632196.png
.. |image5| image:: /_static/images/en-us_image_0000001532472724.png
