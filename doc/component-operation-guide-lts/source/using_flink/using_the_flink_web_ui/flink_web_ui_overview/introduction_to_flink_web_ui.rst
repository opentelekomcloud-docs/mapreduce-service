:original_name: mrs_01_24016.html

.. _mrs_01_24016:

Introduction to Flink Web UI
============================

Flink web UI provides a web-based visual development platform. You only need to compile SQL statements to develop jobs, slashing the job development threshold. In addition, the exposure of platform capabilities allows service personnel to compile SQL statements for job development to quickly respond to requirements, greatly reducing the Flink job development workload.

Flink Web UI Features
---------------------

The Flink web UI has the following features:

-  Enterprise-class visual O&M: GUI-based O&M management, job monitoring, and standardization of Flink SQL statements for job development.
-  Quick cluster connection: After configuring the client and user credential key file, you can quickly access a cluster using the cluster connection function.
-  Quick data connection: You can access a component by configuring the data connection function. If **Data Connection Type** is set to **HDFS**, you need to create a cluster connection. If **Authentication Mode** is set to **KERBEROS** for other data connection types, you need to create a cluster connection. If **Authentication Mode** is set to **SIMPLE**, you do not need to create a cluster connection.
-  Visual development platform: The input/output mapping table can be customized to meet the requirements of different input sources and output destinations.
-  Easy to use GUI-based job management

Key Web UI Capabilities
-----------------------

:ref:`Table 1 <mrs_01_24016__en-us_topic_0000001173949848_table91592142421>` shows the key capabilities provided by Flink web UI.

.. _mrs_01_24016__en-us_topic_0000001173949848_table91592142421:

.. table:: **Table 1** Key web UI capabilities

   +------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item                               | Description                                                                                                                                                                                                                               |
   +====================================+===========================================================================================================================================================================================================================================+
   | Batch-Stream convergence           | -  Batch jobs and stream jobs can be processed with a unified set of Flink SQL statements.                                                                                                                                                |
   +------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Flink SQL kernel capabilities      | -  Flink SQL supports customized window size, stream compute within 24 hours, and batch processing beyond 24 hours.                                                                                                                       |
   |                                    | -  Flink SQL supports Kafka and HDFS reading. Data can be written to Kafka, and HDFS.                                                                                                                                                     |
   |                                    | -  A job can define multiple Flink SQL jobs, and multiple metrics can be combined into one job for computing. If a job contains same primary keys as well as same inputs and outputs, the job supports the computing of multiple windows. |
   |                                    | -  The AVG, SUM, COUNT, MAX, and MIN statistical methods are supported.                                                                                                                                                                   |
   +------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Flink SQL functions on the console | -  Cluster connection management allows you to configure clusters where services such as Kafka, and HDFS reside.                                                                                                                          |
   |                                    | -  Data connection management allows you to configure services such as Kafka, and HDFS.                                                                                                                                                   |
   |                                    | -  Data table management allows you to define data tables accessed by SQL statements and generate DDL statements.                                                                                                                         |
   |                                    | -  Flink SQL job definition allows you to verify, parse, optimize, convert a job into a Flink job, and submit the job for running based on the entered SQL statements.                                                                    |
   +------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Flink job visual management        | -  Stream jobs and batch jobs can be defined in a visual manner.                                                                                                                                                                          |
   |                                    | -  Job resources, fault recovery policies, and checkpoint policies can be configured in a visual manner.                                                                                                                                  |
   |                                    | -  Status monitoring of stream and batch jobs are supported.                                                                                                                                                                              |
   |                                    | -  The Flink job O&M is enhanced, including redirection of the native monitoring page.                                                                                                                                                    |
   +------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Performance and reliability        | -  Stream processing supports 24-hour window aggregation computing and millisecond-level performance.                                                                                                                                     |
   |                                    | -  Batch processing supports 90-day window aggregation computing, which can be completed in minutes.                                                                                                                                      |
   |                                    | -  Invalid data of stream processing and batch processing can be filtered out.                                                                                                                                                            |
   |                                    | -  When HDFS data is read, the data can be filtered based on the calculation period in advance.                                                                                                                                           |
   |                                    | -  If the job definition platform is faulty or the service is degraded, jobs cannot be redefined, but the computing of existing jobs is not affected.                                                                                     |
   |                                    | -  The automatic restart mechanism is provided for job failures. You can configure restart policies.                                                                                                                                      |
   +------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
