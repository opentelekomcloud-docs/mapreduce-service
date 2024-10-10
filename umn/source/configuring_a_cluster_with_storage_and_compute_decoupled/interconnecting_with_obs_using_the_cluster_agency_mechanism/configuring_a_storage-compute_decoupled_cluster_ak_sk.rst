:original_name: mrs_01_0468.html

.. _mrs_01_0468:

Configuring a Storage-Compute Decoupled Cluster (AK/SK)
=======================================================

In MRS 1.9.2 or later, OBS can be interconnected with MRS using **obs://**. Currently, Hadoop, Hive, Spark, Presto, and Flink are supported. HBase cannot use **obs://** to interconnect with OBS.

MRS provides the following configuration modes for accessing OBS. You can select one of them. The agency mode is recommended.

-  Bind an agency of the ECS type to an MRS cluster to access OBS, preventing the AK/SK from being exposed in the configuration file. For details, see :ref:`Configuring a Storage-Compute Decoupled Cluster (Agency) <mrs_01_0768>`.
-  Configure the AK/SK in an MRS cluster. The AK/SK will be exposed in the configuration file in plaintext. Exercise caution when performing this operation. For details, see the following part in this section.

.. note::

   -  To improve data write performance, log in to the Manager and choose **Cluster** > **Services** > *Name of the service to be modified* > **Configurations**. Change the value of **fs.obs.buffer.dir** to the data disk directory.

   -  In the storage-compute decoupled scenario, the OBS parallel file system must be used to configure a cluster. Using common object buckets will greatly affect the cluster performance.

   -  **In MRS 3.2.0-LTS.1 and later versions, components prevent mis-deletion by default. That is, file data deleted by component users is not directly deleted but stored in the recycle bin directory in the OBS file system.**

      To save OBS space, you need to enable periodical deletion of file data from the OBS recycle bin by referring to :ref:`Configuring the Policy for Clearing Component Data in the Recycle Bin <mrs_01_249150>`.

   -  Configuration files containing authentication passwords pose security risks. Delete such files after configuration or store them securely.
   -  Commands carrying authentication passwords pose security risks. Disable historical command recording before running such commands to prevent information leakage.

Using Hadoop to Access OBS
--------------------------

-  Add the following content to file **core-site.xml** in the HDFS directory (**$client_home/ HDFS/hadoop/etc/hadoop**) on the MRS client:

   .. code-block::

      <property>
          <name>fs.obs.access.key</name>
          <value>ak</value>
      </property>
      <property>
          <name>fs.obs.secret.key</name>
          <value>sk</value>
      </property>
      <property>
          <name>fs.obs.endpoint</name>
          <value>obs endpoint</value>
      </property>

   .. important::

      AK and SK will be displayed as plaintext in the configuration file. Exercise caution when setting AK and SK in the file.

   After the configuration is added, you can directly access data on OBS without manually adding the AK/SK and endpoint. For example, run the following command to view the file list of the **test_obs_orc** directory in the **obs-test** file system:

   **hadoop fs -ls "obs://obs-test/test_obs_orc"**

-  Add AK/SK and endpoint to the command line to access data on OBS.

   **hadoop fs -Dfs.obs.endpoint=xxx -Dfs.obs.access.key=xx -Dfs.obs.secret.key=xx -ls "obs://obs-test/ test_obs_orc"**

.. _mrs_01_0468__section1164714235144:

Using Hive to Access OBS
------------------------

#. The Hive service configuration page is displayed.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager, choose **Services** > **Hive** > **Service Configuration**, and select **All** from the **Basic** drop-down list.
   -  For MRS 1.9.2 or later, click the cluster name on the MRS console, choose **Components** > **Hive** > **Service Configuration**, and select **All** from the **Basic** drop-down list.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   -  For MRS 3.\ *x* or later, log in to MRS Manager. For details, see :ref:`Accessing MRS Manager <mrs_01_0129>`. And choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Configurations** > **All Configurations**.

#. In the configuration type drop-down box, switch **Basic Configurations** to **All Configurations**.

#. Search for **fs.obs.access.key** and **fs.obs.secret.key** and set them to the AK and SK of OBS respectively.

   If the preceding two parameters cannot be found in the current cluster, choose **Hive > Customization** in the navigation tree on the left and add the two parameters to the customized parameter **core.site.customized.configs**.

#. Click **Save Configuration** and select **Restart the affected services or instances**. to restart the Hive service.

#. Access the OBS directory in the beeline. For example, run the following command to create a Hive table and specify that data is stored in the **test_obs** directory in the **test-bucket** file system:

   **create table test_obs(a int, b string) row format delimited fields terminated by "," stored as textfile location "obs://test-bucket/test_obs";**

Using Spark to Access OBS
-------------------------

.. note::

   SparkSQL depends on Hive. Therefore, when configuring OBS on Spark, you need to modify the OBS configuration used in :ref:`Using Hive to Access OBS <mrs_01_0468__section1164714235144>`.

-  spark-beeline and spark-sql

   You can add the following OBS attributes to the shell to access OBS:

   .. code-block::

      set fs.obs.endpoint=xxx
      set fs.obs.access.key=xxx
      set fs.obs.secret.key=xxx

-  spark-beeline

   The spark-beeline can access OBS by configuring service parameters on Manager. The procedure is as follows:

   #. Go to the Spark configuration page.

      -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services** > **Spark** > **Service Configuration**.
      -  For MRS 1.9.2 or later, click the cluster name on the MRS console and choose **Components** > **Spark** > **Service Configuration**.

         .. note::

            If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

      -  For MRS 3.\ *x* or later, log in to MRS Manager. For details, see :ref:`Accessing MRS Manager <mrs_01_0129>`. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Configurations**.

   #. In the configuration type drop-down box, switch **Basic Configurations** to **All Configurations**.

   #. Choose **JDBCServer** > **OBS**, and set values for **fs.obs.access.key** and **fs.obs.secret.key**.

      If the preceding two parameters cannot be found in the current cluster, choose **JDBCServer** > **Customization** in the navigation tree on the left and add the two parameters to the customized parameter **spark.core-site.customized.configs**.


      .. figure:: /_static/images/en-us_image_0000001295738100.png
         :alt: **Figure 1** Parameters for adding an OBS

         **Figure 1** Parameters for adding an OBS

   #. Click **Save Configuration** and select **Restart the affected services or instances**. Restart the Spark service.

   #. Access OBS in **spark-beeline**. For example, access the **obs://obs-demo-input/table/** directory.

      **create table test(id int) location 'obs://obs-demo-input/table/';**

-  spark-sql and spark-submit

   The spark-sql can also access OBS by modifying the **core-site.xml** configuration file.

   The method of modifying the configuration file is the same when you use the spark-sql and spark-submit to submit a task to access OBS.

   Add the following content to **core-site.xml** in the Spark configuration folder (**$client_home/Spark/spark/conf**) on the MRS client:

   .. code-block::

      <property>
          <name>fs.obs.access.key</name>
          <value>ak</value>
      </property>
      <property>
          <name>fs.obs.secret.key</name>
          <value>sk</value>
      </property>
      <property>
          <name>fs.obs.endpoint</name>
          <value>obs endpoint</value>
      </property>

Using Presto to Access OBS
--------------------------

#. Go to the cluster details page and choose **Components** > **Presto** > **Service Configuration**.

#. In the configuration type drop-down box, switch **Basic Configurations** to **All Configurations**.

#. Search for and configure the following parameters:

   -  Set **fs.obs.access.key** to **AK**.
   -  Set **fs.obs.secret.key** to **SK**.

   If the preceding two parameters cannot be found in the current cluster, choose **Presto > Hive** in the navigation tree on the left and add the two parameters to the customized parameter **core.site.customized.configs**.

#. Click **Save Configuration** and select **Restart the affected services or instances**. to restart the Presto service.

#. Choose **Components** > **Hive** > **Service Configuration**.

#. In the configuration type drop-down box, switch **Basic Configurations** to **All Configurations**.

#. Search for and configure the following parameters:

   -  Set **fs.obs.access.key** to **AK**.
   -  Set **fs.obs.secret.key** to **SK**.

#. Click **Save Configuration** and select **Restart the affected services or instances**. to restart the Hive service.

#. On the Presto client, run the following statement to create a schema and set **location** to an OBS path:

   **CREATE SCHEMA hive.demo WITH (location = 'obs://obs-demo/presto-demo/');**

#. Create a table in the schema. The table data is stored in the OBS file system. The following is an example.

   **CREATE TABLE hive.demo.demo_table WITH (format = 'ORC') AS SELECT \* FROM tpch.sf1.customer;**

Using Flink to Access OBS
-------------------------

Add the following configuration to the Flink configuration file of the MRS client in **Client installation path/Flink/flink/conf/flink-conf.yaml**:

.. code-block::

   fs.obs.access.key:ak
   fs.obs.secret.key: sk
   fs.obs.endpoint: obs endpoint

.. important::

   AK and SK will be displayed as plaintext in the configuration file. Exercise caution when setting AK and SK in the file.

After the configuration is added, you can directly access data on OBS without manually adding the AK/SK and endpoint.
