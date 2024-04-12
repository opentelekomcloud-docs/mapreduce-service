:original_name: mrs_01_24232.html

.. _mrs_01_24232:

Using CDL from Scratch
======================

CDL supports data synchronization or comparison tasks in multiple scenarios. This section describes how to import data from PgSQL to Kafka on the CDLService WebUI of a cluster with Kerberos authentication enabled.

Prerequisites
-------------

-  The CDL and Kafka services have been installed in a cluster and are running properly.
-  Write-ahead logging is enabled for the PostgreSQL database. For details, see :ref:`Policy for Modifying Write-Ahead Logs in PostgreSQL Databases <mrs_01_24124__li1868193914169>`.
-  You have created a human-machine user, for example, **cdluser**, added the user to user groups **cdladmin** (primary group), **hadoop**, and **kafka**, and associated the user with the **System_administrator** role on FusionInsight Manager.

Procedure
---------

#. Log in to FusionInsight Manager as user **cdluser** (change the password upon the first login) and choose **Cluster** > **Services** > **CDL**. On the **Dashboard** page, click the hyperlink next to **CDLService UI** to go to the native CDL page.

#. Choose **Link Management** and click **Add Link**. On the displayed dialog box, set parameters for adding the **pgsql** and **kafka** links by referring to the following tables.

   .. table:: **Table 1** PgSQL data link parameters

      =========== ===========================
      Parameter   Example Value
      =========== ===========================
      Link Type   pgsql
      Name        pgsqllink
      Host        10.10.10.10
      Port        5432
      DB Name     testDB
      User        user
      Password    *Password of the user user*
      Description ``-``
      =========== ===========================

   .. table:: **Table 2** Kafka data link parameters

      =========== =============
      Parameter   Example Value
      =========== =============
      Link Type   kafka
      Name        kafkalink
      Description ``-``
      =========== =============

#. After the parameters are configured, click **Test** to check whether the data link is normal.

   After the test is successful, click **OK**.

#. .. _mrs_01_24232__li8419191320242:

   On the **Job Management** page, click **Add Job**. In the displayed dialog box, configure the parameters and click **Next**.

   Specifically:

   ========= ================
   Parameter Example Value
   ========= ================
   Name      job_pgsqltokafka
   Desc      xxx
   ========= ================

#. Configure PgSQL job parameters.

   a. On the **Job Management** page, drag the **pgsql** icon on the left to the editing area on the right and double-click the icon to go to the PgSQL job configuration page.

      .. table:: **Table 3** PgSQL job parameters

         ===================== ==========================
         Parameter             Example Value
         ===================== ==========================
         Link                  pgsqllink
         Tasks Max             1
         Mode                  insert, update, and delete
         Schema                public
         dbName Alias          cdc
         Slot Name             a4545sad
         Slot Drop             No
         Connect With Hudi     No
         Use Exist Publication Yes
         Publication Name      test
         ===================== ==========================

   b. Click the plus sign (+) to display more parameters.

      |image1|

      .. note::

         -  **WhiteList**: Enter the name of the table in the database, for example, **myclass**.
         -  **Topic Table Mapping**: In the first text box, enter a topic name (the value must be different from that of **Name** in :ref:`4 <mrs_01_24232__li8419191320242>`), for example, **myclass_topic**. In the second text box, enter a table name, for example, **myclass**. The value must be in one-to-one relationship with the topic name entered in the first text box.)

   c. Click **OK**. The PgSQL job parameters are configured.

#. Configure Kafka job parameters.

   a. On the **Job Management** page, drag the **kafka** icon on the left to the editing area on the right and double-click the icon to go to the Kafka job configuration page. Configure parameters based on :ref:`Table 4 <mrs_01_24232__table8128935153416>`.

      .. _mrs_01_24232__table8128935153416:

      .. table:: **Table 4** Kafka job parameter

         ========= =============
         Parameter Example Value
         ========= =============
         Link      kafkalink
         ========= =============

   b. Click **OK**.

#. After the job parameters are configured, drag the two icons to associate the job parameters and click **Save**. The job configuration is complete.

   |image2|

#. In the job list on the **Job Management** page, locate the created jobs, click **Start** in the **Operation** column, and wait until the jobs are started.

   Check whether the data transmission takes effect. For example, insert data into the table in the PgSQL database, go to the Kafka UI to check whether data is generated in the Kafka topic by referring to :ref:`Managing Topics on Kafka UI <mrs_01_24138>`.

.. |image1| image:: /_static/images/en-us_image_0000001532951860.png
.. |image2| image:: /_static/images/en-us_image_0000001583151841.png
