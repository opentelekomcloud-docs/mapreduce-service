:original_name: mrs_01_24751.html

.. _mrs_01_24751:

Synchronizing Data from MySQL to Hudi
=====================================

Scenario
--------

This section describes how to import data from MySQL to Hudi by using the CDLService web UI of a cluster with Kerberos authentication enabled.

Prerequisites
-------------

-  The CDL and Hudi services have been installed in a cluster and are running properly.
-  The prerequisites for the MySQL database have been met. For details, see :ref:`Prerequisites for Enabling the MySQL Database <mrs_01_24124__li268123915168>`.
-  You have created a human-machine user, for example, **cdluser**, added the user to user groups **cdladmin** (primary group), **hadoop**, **kafka**, and **supergroup**, and associated the user with the **System_administrator** role on FusionInsight Manager.

Procedure
---------

#. Log in to FusionInsight Manager as user **cdluser** (change the password upon your first login), choose **Cluster** > **Services** > **CDL**, and click the link next to **CDLService UI** to go to the CDLService web UI.

#. Choose **Driver Management** and click **Upload Driver** to upload the driver file **mysql-connector-java-8.0.24.jar** of MySQL. For details, see :ref:`Uploading a Driver File <mrs_01_24237>`.

#. Choose **Link Management** and click **Add Link**. In the displayed dialog box, set parameters for adding the **mysql** and **hudi** links by referring to the following tables.

   .. table:: **Table 1** MySQL data link parameters

      =========== ===============================
      Parameter   Example
      =========== ===============================
      Link Type   mysql
      Name        mysqllink
      DB driver   mysql-connector-java-8.0.24.jar
      Host        10.10.10.10
      Port        3306
      User        dbuser
      Password    *Password of the dbuser user*
      Description ``-``
      =========== ===============================

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

   ========= ===============
   Parameter Example
   ========= ===============
   Name      job_mysqltohudi
   Desc      ``-``
   ========= ===============

#. Configure MySQL job parameters.

   a. On the **Job Management** page, drag the **mysql** icon on the left to the editing area on the right and double-click the icon to go to the MySQL job configuration page. Configure parameters based on the following table.

      .. table:: **Table 4** MySQL job parameters

         ================== ==========================
         Parameter          Example
         ================== ==========================
         Link               mysqllink
         Tasks Max          1
         Mode               insert, update, and delete
         DB Name            MYSQLDBA
         Schema Auto Create Yes
         Connect With Hudi  Yes
         ================== ==========================

   b. Click the plus sign (+) to display more parameters.

      |image1|

      .. note::

         -  **PosFromBeginning**: whether to capture CDC events from the start position
         -  **DBZ Snapshot Locking Mode**: lock mode when the connector is performing a snapshot. **none** indicates that no lock is held during the snapshot.
         -  **WhiteList**: Enter the database table to receive data, for example, **myclass**.
         -  **Blacklist**: Enter the database table that does not need to capture data.
         -  **Multi Partition**: whether to enable Kafka partitioning.
         -  **Topic Table Mapping**

            -  This parameter is mandatory if **Connect With Hudi** is set to **Yes**.
            -  Enter the table name in the first text box, for example, **test**. Enter a topic name in the second text box, for example, **test_topic**. The topic name must match the table name in the first text box.

   c. Click **OK**. The MySQL job parameters are configured.

#. Configure Hudi job parameters.

   a. On the **Job Management** page, drag the **hudi** icon in the Sink area on the left to the editing area on the right and double-click the icon to go to the Hudi job configuration page. Configure parameters based on the following table:

      .. table:: **Table 5** Sink Hudi job parameters

         +-------------------------------------------------------------------------+---------------+
         | Parameter                                                               | Example Value |
         +=========================================================================+===============+
         | Link                                                                    | hudilink      |
         +-------------------------------------------------------------------------+---------------+
         | Path                                                                    | /cdl/test     |
         +-------------------------------------------------------------------------+---------------+
         | Interval                                                                | 10            |
         +-------------------------------------------------------------------------+---------------+
         | Max Rate Per Partition                                                  | 0             |
         +-------------------------------------------------------------------------+---------------+
         | Parallelism                                                             | 10            |
         +-------------------------------------------------------------------------+---------------+
         | Target Hive Database                                                    | default       |
         +-------------------------------------------------------------------------+---------------+
         | Configuring Hudi Table Attributes                                       | Visual View   |
         +-------------------------------------------------------------------------+---------------+
         | Global Configuration of Hudi Table Attributes                           | ``-``         |
         +-------------------------------------------------------------------------+---------------+
         | Configuring the Attributes of the Hudi Table: Table Name                | test          |
         +-------------------------------------------------------------------------+---------------+
         | Configuring the Attributes of the Hudi Table: Table Type Opt Key        | COPY_ON_WRITE |
         +-------------------------------------------------------------------------+---------------+
         | Configuring the Attributes of the Hudi Table: Hudi TableName Mapping    | ``-``         |
         +-------------------------------------------------------------------------+---------------+
         | Configuring the Attributes of the Hudi Table: Hive TableName Mapping    | ``-``         |
         +-------------------------------------------------------------------------+---------------+
         | Configuring the Attributes of the Hudi Table: Table Primarykey Mapping  | id            |
         +-------------------------------------------------------------------------+---------------+
         | Configuring the Attributes of the Hudi Table: Table Hudi Partition Type | ``-``         |
         +-------------------------------------------------------------------------+---------------+
         | Configuring the Attributes of the Hudi Table: Custom Config             | ``-``         |
         +-------------------------------------------------------------------------+---------------+

      |image2|

   b. (Optional) Click the plus sign (+) to display the **Execution Env** parameter. Select a created environment for it. The default value is **defaultEnv**.

      |image3|

   c. Click **OK**.

#. Drag the two icons to associate the job parameters and click **Save**. The job configuration is complete.

   |image4|

#. In the job list on the **Job Management** page, locate the created job, click **Start** in the **Operation** column, and wait until the job is started.

   Check whether the data transmission takes effect, for example, insert data into the table in the MySQL database and view the content of the file imported to Hudi.

.. |image1| image:: /_static/images/en-us_image_0000001532632200.png
.. |image2| image:: /_static/images/en-us_image_0000001537076386.png
.. |image3| image:: /_static/images/en-us_image_0000001587875989.png
.. |image4| image:: /_static/images/en-us_image_0000001532472728.png
