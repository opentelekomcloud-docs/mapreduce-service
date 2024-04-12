:original_name: mrs_01_24753.html

.. _mrs_01_24753:

Synchronizing Data from Hudi to DWS
===================================

Scenario
--------

This section describes how to import data from Hudi to DWS by using the CDLService web UI of a cluster with Kerberos authentication enabled.

Prerequisites
-------------

-  The CDL and Hudi services have been installed in a cluster and are running properly.
-  The prerequisites for the DWS database have been met. For details, see :ref:`Prerequisites for the DWS database <mrs_01_24124__li6127144552014>`.
-  You have created a human-machine user, for example, **cdluser**, added the user to user groups **cdladmin** (primary group), **hadoop**, **kafka**, and **supergroup**, and associated the user with the **System_administrator** role on FusionInsight Manager.

Procedure
---------

#. Log in to FusionInsight Manager as user **cdluser** (change the password upon your first login), choose **Cluster** > **Services** > **CDL**, and click the link next to **CDLService UI** to go to the CDLService web UI.

#. Choose **Link Management** and click **Add Link**. In the displayed dialog box, set parameters for adding the **dws** and **hudi** links by referring to the following tables.

   .. table:: **Table 1** DWS data link parameters

      =========== ===================================
      Parameter   Example
      =========== ===================================
      Link Type   dws
      Name        dwstest
      Host        10.10.10.10
      Port        8000
      DB Name     dwsdb
      User        dbuser
      Password    *Password of the* **dbuser** *user*
      Description ``-``
      =========== ===================================

   .. table:: **Table 2** Hudi data link parameters

      =============== ===================================================
      Parameter       Example
      =============== ===================================================
      Link Type       hudi
      Name            hudilink
      Storage Type    hdfs
      Auth KeytabFile /opt/Bigdata/third_lib/CDL/user_libs/cdluser.keytab
      Principal       cdluser
      Description     xxx
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

   ========= =============
   Parameter Example
   ========= =============
   Name      job_huditodws
   Desc      ``-``
   ========= =============

#. Configure Hudi job parameters.

   a. On the **Job Management** page, drag the **hudi** icon in the Source area on the left to the editing area on the right and double-click the icon to go to the Hudi job configuration page. Configure parameters based on the following table.

      .. table:: **Table 4** Source Hudi job parameters

         +------------+--------------------------------------------------------------------------------------------------------+
         | Parameter  | Example                                                                                                |
         +============+========================================================================================================+
         | Link       | hudilink                                                                                               |
         +------------+--------------------------------------------------------------------------------------------------------+
         | Interval   | 10                                                                                                     |
         +------------+--------------------------------------------------------------------------------------------------------+
         | Table Info | {"table1":[{"source.database":"dwsdb","source.tablename":"tabletest","target.tablename":"tabletest"}]} |
         +------------+--------------------------------------------------------------------------------------------------------+

      |image1|

   b. Click **OK**. The Hudi job parameters are configured.

#. Configure DWS job parameters.

   a. On the **Job Management** page, drag the **dws** icon on the left to the editing area on the right and double-click the icon to go to the DWS job configuration page. Configure parameters based on the following table.

      .. table:: **Table 5** DWS job parameters

         ============= =======
         Parameter     Example
         ============= =======
         Link          dwstest
         Query Timeout 180000
         Batch Size    10
         ============= =======

      .. note::

         -  Data can be synchronized from Hudi to GaussDB(DWS) only when both Hudi and GaussDB(DWS) contain the **precombine** field.

         -  GaussDB(DWS) tables must contain the **precombine** field and the primary key.

         -  By default, the Hudi built-in field **\_hoodie_event_time** is used. If this field is not used, **enable.sink.precombine** must be specified. An example is as follows:

            |image2|

   b. Click **OK**.

#. Drag the two icons to associate the job parameters and click **Save**. The job configuration is complete.

   |image3|

#. In the job list on the **Job Management** page, locate the created job, click **Start** in the **Operation** column, and wait until the job is started.

   Check whether the data transmission takes effect, for example, insert data into the Hudi table and view the content of the file imported to DWS.

.. |image1| image:: /_static/images/en-us_image_0000001532632204.png
.. |image2| image:: /_static/images/en-us_image_0000001532472732.png
.. |image3| image:: /_static/images/en-us_image_0000001532791952.png
