:original_name: mrs_01_1449.html

.. _mrs_01_1449:

SET/RESET
=========

Function
--------

This command is used to dynamically add, update, display, or reset the CarbonData properties without restarting the driver.

Syntax
------

-  Add or Update parameter value:

   **SET** *parameter_name*\ =\ *parameter_value*

   This command is used to add or update the value of **parameter_name**.

-  Display property value:

   **SET** *parameter_name*

   This command is used to display the value of **parameter_name**.

-  Display session parameter:

   **SET**

   This command is used to display all supported session parameters.

-  Display session parameters along with usage details:

   **SET** -v

   This command is used to display all supported session parameters and their usage details.

-  Reset parameter value:

   **RESET**

   This command is used to clear all session parameters.

Parameter Description
---------------------

.. table:: **Table 1** SET parameters

   +-----------------+----------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                            |
   +=================+========================================================================================+
   | parameter_name  | Name of the parameter whose value needs to be dynamically added, updated, or displayed |
   +-----------------+----------------------------------------------------------------------------------------+
   | parameter_value | New value of **parameter_name** to be set                                              |
   +-----------------+----------------------------------------------------------------------------------------+

Precautions
-----------

The following table lists the properties which you can set or clear using the SET or RESET command.

.. table:: **Table 2** Properties

   +------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Property                                 | Description                                                                                                                                                                                                    |
   +==========================================+================================================================================================================================================================================================================+
   | carbon.options.bad.records.logger.enable | Whether to enable bad record logger.                                                                                                                                                                           |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | carbon.options.bad.records.action        | Operations on bad records, for example, force, redirect, fail, or ignore. For more information, see :ref:`•Bad record handling <mrs_01_1438__en-us_topic_0000001219149099_lcf623574402c443e908646591898c2be>`. |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | carbon.options.is.empty.data.bad.record  | Whether the empty data is considered as a bad record. For more information, see :ref:`Bad record handling <mrs_01_1438__en-us_topic_0000001219149099_lcf623574402c443e908646591898c2be>`.                      |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | carbon.options.sort.scope                | Scope of the sort during data loading.                                                                                                                                                                         |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | carbon.options.bad.record.path           | HDFS path where bad records are stored.                                                                                                                                                                        |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | carbon.custom.block.distribution         | Whether to enable Spark or CarbonData block distribution.                                                                                                                                                      |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | enable.unsafe.sort                       | Whether to use unsafe sort during data loading. Unsafe sort reduces the garbage collection during data loading, thereby achieving better performance.                                                          |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | carbon.si.lookup.partialstring           | If this is set to **TRUE**, the secondary index uses the starts-with, ends-with, contains, and LIKE partition condition strings.                                                                               |
   |                                          |                                                                                                                                                                                                                |
   |                                          | If this is set to **FALSE**, the secondary index uses only the starts-with partition condition string.                                                                                                         |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | carbon.input.segments                    | Segment ID to be queried. This property allows you to query a specified segment of a specified table. CarbonScan reads data only from the specified segment ID.                                                |
   |                                          |                                                                                                                                                                                                                |
   |                                          | Syntax:                                                                                                                                                                                                        |
   |                                          |                                                                                                                                                                                                                |
   |                                          | **carbon.input.segments. <database_name>. <table_name> = < list of segment ids >**                                                                                                                             |
   |                                          |                                                                                                                                                                                                                |
   |                                          | If you want to query a specified segment in multi-thread mode, you can use **CarbonSession.threadSet** instead of the **SET** statement.                                                                       |
   |                                          |                                                                                                                                                                                                                |
   |                                          | Syntax:                                                                                                                                                                                                        |
   |                                          |                                                                                                                                                                                                                |
   |                                          | **CarbonSession.threadSet ("carbon.input.segments. <database_name>. <table_name>","< list of segment ids >");**                                                                                                |
   |                                          |                                                                                                                                                                                                                |
   |                                          | .. note::                                                                                                                                                                                                      |
   |                                          |                                                                                                                                                                                                                |
   |                                          |    You are advised not to set this property in the **carbon.properties** file because all sessions contain the segment list unless session-level or thread-level overwriting occurs.                           |
   +------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Examples
--------

-  Add or Update:

   **SET** *enable.unsafe.sort*\ =\ *true*

-  Display property value:

   **SET** *enable.unsafe.sort*

-  Show the segment ID list, segment status, and other required details, and specify the segment list to be read:

   **SHOW SEGMENTS FOR** *TABLE carbontable1;*

   **SET** *carbon.input.segments.db.carbontable1 = 1, 3, 9;*

-  Query a specified segment in multi-thread mode:

   **CarbonSession.threadSet** (*"carbon.input.segments.default.carbon_table_MulTI_THread", "1,3"*);

-  Use **CarbonSession.threadSet** to query segments in a multi-thread environment (Scala code is used as an example):

   .. code-block::

      def main(args: Array[String]) {
       Future {              CarbonSession.threadSet("carbon.input.segments.default.carbon_table_MulTI_THread", "1")
            spark.sql("select count(empno) from carbon_table_MulTI_THread").show()
          }
      }

-  Reset:

   **RESET**

System Response
---------------

-  Success will be recorded in the driver log.
-  Failure will be displayed on the UI.
