:original_name: mrs_01_24754.html

.. _mrs_01_24754:

Synchronizing Data from Hudi to ClickHouse
==========================================

Scenario
--------

This section describes how to import data from Hudi to ClickHouse by using the CDLService web UI of a cluster with Kerberos authentication enabled.

Prerequisites
-------------

-  The CDL, Hudi, and ClickHouse services have been installed in a cluster and are running properly.
-  You have operation permissions on ClickHouse. For details, see :ref:`ClickHouse User and Permission Management <mrs_01_24057>`.
-  You have created a human-machine user with the ClickHouse administrator permissions (for details, see :ref:`ClickHouse User and Permission Management <mrs_01_24057>`), for example, **cdluser**, added the user to user groups **cdladmin** (primary group), **hadoop**, **kafka**, and **supergroup**, and associated the user with the **System_administrator** role on FusionInsight Manager.
-  You have manually created a local table and distributed table on ClickHouse. The local table uses the ReplicatedReplacingMergeTree engine. For details, see :ref:`Creating a ClickHouse Table <mrs_01_2398>`.

Procedure
---------

#. Log in to FusionInsight Manager as user **cdluser** (change the password upon your first login), choose **Cluster** > **Services** > **CDL**, and click the link next to **CDLService UI** to go to the CDLService web UI.

#. Choose **Link Management** and click **Add Link**. In the displayed dialog box, set parameters for adding the **clickhouse** and **hudi** links by referring to the following tables.

   .. table:: **Table 1** ClickHouse data link parameters

      =========== ====================================
      Parameter   Example
      =========== ====================================
      Link Type   clickhouse
      Name        cklink
      Host        10.10.10.10:21428
      User        *cdluser*
      Password    *Password of the* **cdluser** *user*
      Description ``-``
      =========== ====================================

   .. table:: **Table 2** Hudi data link parameters

      =============== ===================================================
      Parameter       Example
      =============== ===================================================
      Link Type       hudi
      Name            hudilink
      Storage Type    hdfs
      Auth KeytabFile /opt/Bigdata/third_lib/CDL/user_libs/cdluser.keytab
      Principal       cdluser
      Description     ``-``
      =============== ===================================================

#. After the parameters are configured, click **Test** to check whether the data link is normal.

   After the test is successful, click **OK**.

#. (Optional) Choose **ENV Management** and click **Add Env**. In the displayed dialog box, configure the parameters based on the following table.

   .. table:: **Table 3** Parameters for adding an ENV

      ================ =============
      Parameter        Example Value
      ================ =============
      Name             test-env
      Driver Memory    1 GB
      Type             spark
      Executor Memory  1 GB
      Executor Cores   1
      Number Executors 1
      Queue            ``-``
      Description      ``-``
      ================ =============

   Click **OK**.

#. Choose **Job Management** > **Data synchronization task** and click **Add Job**. In the displayed dialog box, set parameters and click **Next**.

   Parameters are as follows.

   ========= ============
   Parameter Example
   ========= ============
   Name      job_huditock
   Desc      ``-``
   ========= ============

#. Configure Hudi job parameters.

   a. On the **Job Management** page, drag the **hudi** icon in the Source area on the left to the editing area on the right and double-click the icon to go to the Hudi job configuration page. Configure parameters based on the following table.

      .. table:: **Table 4** Source Hudi job parameters

         +------------+-------------------------------------------------------------------------------------------------------------+
         | Parameter  | Example                                                                                                     |
         +============+=============================================================================================================+
         | Link       | hudilink                                                                                                    |
         +------------+-------------------------------------------------------------------------------------------------------------+
         | Interval   | 10                                                                                                          |
         +------------+-------------------------------------------------------------------------------------------------------------+
         | Table Info | {"table1":[{"source.database":"db","source.tablename":"tabletest","target.tablename":"default.tabletest"}]} |
         +------------+-------------------------------------------------------------------------------------------------------------+

      |image1|

   b. Click **OK**. The Hudi job parameters are configured.

#. Configure ClickHouse job parameters.

   a. On the **Job Management** page, drag the **clickhouse** icon on the left to the editing area on the right and double-click the icon to go to the ClickHouse job configuration page. Configure parameters based on the following table.

      .. table:: **Table 5** ClickHouse job parameters

         ============= =======
         Parameter     Example
         ============= =======
         Link          cklink
         Query Timeout 60000
         Batch Size    100
         ============= =======

      |image2|

   b. Click **OK**.

#. Drag the two icons to associate the job parameters and click **Save**. The job configuration is complete.

   |image3|

#. In the job list on the **Job Management** page, locate the created job, click **Start** in the **Operation** column, and wait until the job is started.

   Check whether the data transmission takes effect, for example, insert data into the Hudi table and view the content of the file imported to ClickHouse.

.. |image1| image:: /_static/images/en-us_image_0000001532951888.png
.. |image2| image:: /_static/images/en-us_image_0000001583151869.png
.. |image3| image:: /_static/images/en-us_image_0000001583391865.png
