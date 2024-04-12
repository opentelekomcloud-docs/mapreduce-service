:original_name: mrs_01_24763.html

.. _mrs_01_24763:

Synchronizing Data from ThirdKafka to Hudi
==========================================

Scenario
--------

This section describes how to import data from ThirdKafka to Hudi by using the CDLService web UI of a cluster with Kerberos authentication enabled.

Prerequisites
-------------

-  The CDL and Hudi services have been installed in a cluster and are running properly.
-  Topics of the ThirdKafka database can be consumed by the MRS cluster. For details, see :ref:`PrerequisitesforThirdPartyKafka <mrs_01_24124__li347115587209>`.
-  You have created a human-machine user, for example, **cdluser**, added the user to user groups **cdladmin** (primary group), **hadoop**, **kafka**, and **supergroup**, and associated the user with the **System_administrator** role on FusionInsight Manager.

Procedure
---------

#. Log in to FusionInsight Manager as user **cdluser** (change the password upon your first login), choose **Cluster** > **Services** > **CDL**, and click the link next to **CDLService UI** to go to the CDLService web UI.

#. Choose **Link Management** and click **Add Link**. In the displayed dialog box, set parameters for adding the **thirdparty-kafka** and **hudi** links by referring to the following tables.

   .. table:: **Table 1** thirdparty-kafka data link parameters

      +-------------------------+-----------------------------------------------------+
      | Parameter               | Example                                             |
      +=========================+=====================================================+
      | Name                    | opengausslink                                       |
      +-------------------------+-----------------------------------------------------+
      | Link Type               | thirdparty-kafka                                    |
      +-------------------------+-----------------------------------------------------+
      | Bootstrap Servers       | 10.10.10.10:9093                                    |
      +-------------------------+-----------------------------------------------------+
      | Security Protocol       | SASL_SSL                                            |
      +-------------------------+-----------------------------------------------------+
      | Username                | testuser                                            |
      +-------------------------+-----------------------------------------------------+
      | Password                | *Password of the* **testuser** *user*               |
      +-------------------------+-----------------------------------------------------+
      | SSL Truststore Location | Click **Upload** to upload the authentication file. |
      +-------------------------+-----------------------------------------------------+
      | SSL Truststore Password | ``-``                                               |
      +-------------------------+-----------------------------------------------------+
      | Datastore Type          | opengauss                                           |
      +-------------------------+-----------------------------------------------------+
      | Host                    | 11.11.xxx.xxx,12.12.xxx.xxx                         |
      +-------------------------+-----------------------------------------------------+
      | Port                    | 8000                                                |
      +-------------------------+-----------------------------------------------------+
      | DB Name                 | opengaussdb                                         |
      +-------------------------+-----------------------------------------------------+
      | User                    | opengaussuser                                       |
      +-------------------------+-----------------------------------------------------+
      | DB Password             | *Password of the* **opengaussuser** *user*          |
      +-------------------------+-----------------------------------------------------+
      | Description             | ``-``                                               |
      +-------------------------+-----------------------------------------------------+

   .. note::

      MRS Kafka can also be used as the source of thirdparty-kafka. If the username and password are used for login authentication, log in to FusionInsight Manager, choose **Cluster** > **Services** > **Kafka**, click **Configuration**, search for the **sasl.enabled.mechanisms** parameter in the search box, add **PLAIN** as the parameter value, click **Save** to save the configuration, and restart the Kafka service for the configuration to take effect.

      |image1|

      On the CDL web UI, configure the thirdparty-kafka link that uses MRS Kafka as the source. For example, the data link configuration is as follows:

      |image2|

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

   ========= ===================
   Parameter Example
   ========= ===================
   Name      job_opengausstohudi
   Desc      New CDL Job
   ========= ===================

#. Configure ThirdKafka job parameters.

   a. On the **Job Management** page, drag the **thirdparty-kafka** icon on the left to the editing area on the right and double-click the icon to go to the ThirdpartyKafka job configuration page. Configure parameters based on the following table.

      .. table:: **Table 4** thirdparty-kafka job parameters

         =================== ===============
         Parameter           Example
         =================== ===============
         Link                opengausslink
         DB Name             opengaussdb
         Schema              opengaussschema
         Datastore Type      opengauss
         Source Topics       source_topic
         Tasks Max           1
         Tolerance           none
         Start Time          ``-``
         Multi Partition     No
         Topic Table Mapping test/hudi_topic
         =================== ===============

      |image3|

   b. Click **OK**. The ThirdpartyKafka job parameters are configured.

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

      |image4|

   b. (Optional) Click the plus sign (+) to display the **Execution Env** parameter. Select a created environment for it. The default value is **defaultEnv**.

      |image5|

   c. Click **OK**.

#. Drag the two icons to associate the job parameters and click **Save**. The job configuration is complete.

   |image6|

#. In the job list on the **Job Management** page, locate the created job, click **Start** in the **Operation** column, and wait until the job is started.

   Check whether the data transmission takes effect, for example, insert data into the table in the openGauss database and view the content of the file imported to Hudi.

.. |image1| image:: /_static/images/en-us_image_0000001583151865.png
.. |image2| image:: /_static/images/en-us_image_0000001583391861.png
.. |image3| image:: /_static/images/en-us_image_0000001583272169.png
.. |image4| image:: /_static/images/en-us_image_0000001587755985.png
.. |image5| image:: /_static/images/en-us_image_0000001536916934.png
.. |image6| image:: /_static/images/en-us_image_0000001582952097.png
