:original_name: mrs_08_00122.html

.. _mrs_08_00122:

Relationship Between Hue and Other Components
=============================================

Relationship Between Hue and Hadoop Clusters
--------------------------------------------

:ref:`Table 1 <mrs_08_00122__table11348180>` shows how Hue interacts with Hadoop clusters.

.. _mrs_08_00122__table11348180:

.. table:: **Table 1** Relationship Between Hue and Other Components

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Connection Name                   | Description                                                                                                                                                                                                                                                                          |
   +===================================+======================================================================================================================================================================================================================================================================================+
   | HDFS                              | HDFS provides REST APIs to interact with Hue to query and operate HDFS files.                                                                                                                                                                                                        |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   | Hue packages a user request into interface data, sends the request to HDFS through REST APIs, and displays execution results on the web UI.                                                                                                                                          |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Hive                              | Hive provides Thrift interfaces to interact with Hue, execute Hive SQL statements, and query table metadata.                                                                                                                                                                         |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   | If you edit HQL statements on the Hue web UI, then, Hue submits the HQL statements to the Hive server through the Thrift APIs and displays execution results on the web UI.                                                                                                          |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | YARN/MapReduce                    | MapReduce provides REST APIs to interact with Hue and query YARN job information.                                                                                                                                                                                                    |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   | If you go to the Hue web UI, enter the filter parameters, the UI sends the parameters to the background, and Hue invokes the REST APIs provided by MapReduce (MR1/MR2-YARN) to obtain information such as the status of the task running, the start/end time, the run log, and more. |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Oozie                             | Oozie provides REST APIs to interact with Hue, create workflows, coordinators, and bundles, and manage and monitor tasks.                                                                                                                                                            |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   | A graphical workflow, coordinator, and bundle editor are provided on the Hue web UI. Hue invokes the REST APIs of Oozie to create, modify, delete, submit, and monitor workflows, coordinators, and bundles.                                                                         |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ZooKeeper                         | ZooKeeper provides REST APIs to interact with Hue and query ZooKeeper node information.                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                                                      |
   |                                   | ZooKeeper node information is displayed in the Hue web UI. Hue invokes the REST APIs of ZooKeeper to obtain the node information.                                                                                                                                                    |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
