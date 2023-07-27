:original_name: mrs_08_0094.html

.. _mrs_08_0094:

IoTDB Basic Principles
======================

Database for Internet of Things (IoTDB) is a software system that collects, stores, manages, and analyzes IoT time series data. Apache IoTDB uses a lightweight architecture and features high performance and rich functions.

IoTDB sorts time series and stores indexes and chunks, greatly improving the query performance of time series data. IoTDB uses the Raft protocol to ensure data consistency. In time series scenarios, IoTDB pre-computes and stores data to improve analysis performance. Based on the characteristics of time series data, IoTDB provides powerful data encoding and compression capabilities. In addition, its replica mechanism ensures data security. IoTDB is deeply integrated with Apache Hadoop and Flink to meet the requirements of massive data storage, high-speed data reading, and complex data analysis in the industrial IoT field.

IoTDB Architecture
------------------

The IoTDB suite consists of multiple components to provide a series of functions such as data collection, data writing, data storage, data query, data visualization, and data analysis.

:ref:`Figure 1 <mrs_08_0094__fig121405277474>` shows the overall application architecture after all components of the IoTDB suite are used. IoTDB refers to the time series database component in the suite.

.. _mrs_08_0094__fig121405277474:

.. figure:: /_static/images/en-us_image_0000001535888150.png
   :alt: **Figure 1** IoTDB architecture

   **Figure 1** IoTDB architecture

-  Users can use Java Database Connectivity (JDBC) or Session to import the time series data and system status data (such as server load, CPU usage and memory usage) collected from device sensors, as well as time series data in message queues, applications, or other databases, to the local or remote IoTDB. Users can also directly write the preceding data into a local TsFile file or a TsFile file in the HDFS.
-  Users can write TsFile files to the HDFS to implement data processing tasks such as exception detection and machine learning on the Hadoop or Flink data processing platform.
-  The TsFile-Hadoop or TsFile-Flink connector can be used to allow Hadoop or Flink to process the TsFile files written to the HDFS or local host.
-  The analysis result can be written back to a TsFile in the same way.
-  IoTDB and TsFile also provide client tools to meet users' requirements for viewing and writing data in SQL, script, and graphical formats.

The IoTDB service includes two roles: IoTDBServer (DataNode) and ConfigNode. The role name DataNode of the community edition has the same name as the HDFS role. DataNode is renamed IoTDBServer.

-  ConfigNode: management role, which is responsible for DataNode data sharding and load balancing.
-  IoTDBServer (DataNode): storage role, which is responsible for storing, querying, and writing data.


.. figure:: /_static/images/en-us_image_0000001586567997.png
   :alt: **Figure 2** IoTDB distributed architecture

   **Figure 2** IoTDB distributed architecture

IoTDB Principles
----------------

Based on the attribute hierarchy, attribute coverage, and subordinate relationships between data, the IoTDB data model can be represented as the attribute hierarchy, as shown in :ref:`Figure 3 <mrs_08_0094__fig1285721116>`. The hierarchy is as follows: power group layer - power plant layer - device layer - sensor layer. **ROOT** is a root node, and each node at the sensor layer is a leaf node. According to the IoTDB syntax, the path from **ROOT** to a leaf node is separated by a dot (.). The complete path is used to name a time series in the IoTDB. For example, the time series name corresponding to the path on the left in the following figure is **ROOT.ln.wf01.wt01.status**.

.. _mrs_08_0094__fig1285721116:

.. figure:: /_static/images/en-us_image_0000001586807745.jpg
   :alt: **Figure 3** IoTDB data model

   **Figure 3** IoTDB data model
