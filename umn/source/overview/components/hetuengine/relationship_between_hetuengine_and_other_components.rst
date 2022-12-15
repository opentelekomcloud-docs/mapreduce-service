:original_name: mrs_08_00682.html

.. _mrs_08_00682:

Relationship Between HetuEngine and Other Components
====================================================

The HetuEngine installation depends on the MRS cluster. :ref:`Table 1 <mrs_08_00682__en-us_topic_0254454590_table5889013405>` lists the components on which the HetuServer installation depends.

.. _mrs_08_00682__en-us_topic_0254454590_table5889013405:

.. table:: **Table 1** Components on which HetuEngine depends

   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Name      | Description                                                                                                                                                        |
   +===========+====================================================================================================================================================================+
   | HDFS      | Hadoop Distributed File System, supporting high-throughput data access and suitable for applications with large-scale data sets.                                   |
   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Hive      | Open-source data warehouse built on Hadoop. It stores structured data and implements basic data analysis using the Hive Query Language (HQL), a SQL-like language. |
   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | ZooKeeper | Enables highly reliable distributed coordination. It helps prevent single point of failures (SPOFs) and provides reliable services for applications.               |
   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | KrbServer | Key management center that distributes bills.                                                                                                                      |
   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Yarn      | Resource management system, which is a general resource module that manages and schedules resources for various applications.                                      |
   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | DBService | DBService is a high-availability relational database storage system that provides metadata backup and restoration functions.                                       |
   +-----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
