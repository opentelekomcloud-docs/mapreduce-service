:original_name: mrs_01_248993.html

.. _mrs_01_248993:

Interconnecting Hudi with OBS
=============================

Interconnecting with OBS
------------------------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following commands to configure environment variables:

   **source**\ *Client installation directory*\ **/bigdata_env**

   **source** *Client installation directory*\ **/Hudi/component_env**

#. Modify the configuration file.

   **vim** *Client installation directory*\ **/Hudi/hudi/conf/hdfs-site.xml**

   .. code-block::

      <property>
      <name>dfs.namenode.acls.enabled</name>
      <value>false</value>
      </property>

#. If Kerberos authentication has been enabled(security mode) for the cluster, run the following command to perform authentication as a user who has the Read and Write permissions on the corresponding OBS path. If Kerberos authentication has not been enabled (normal mode) for the cluster, you do not need to run this command.

   **kinit** *Username*

#. Start **spark-shell** and run the following commands to create a COW table and store it to OBS:

   **spark-shell --master yarn**

   **import org.apache.hudi.QuickstartUtils.\_**

   **import scala.collection.JavaConversions.\_**

   **import org.apache.spark.sql.SaveMode.\_**

   **import org.apache.hudi.DataSourceReadOptions.\_**

   **import org.apache.hudi.DataSourceWriteOptions.\_**

   **import org.apache.hudi.config.HoodieWriteConfig.\_**

   **val tableName = "hudi_cow_table"**

   **val basePath = "obs://testhudi/cow_table/"**

   **val dataGen = new DataGenerator**

   **val inserts = convertToStringList(dataGen.generateInserts(10))**

   **val df = spark.read.json(spark.sparkContext.parallelize(inserts, 2))**

   **df.write.format("org.apache.hudi").**

   **options(getQuickstartWriteConfigs).**

   **option(PRECOMBINE_FIELD_OPT_KEY, "ts").**

   **option(RECORDKEY_FIELD_OPT_KEY, "uuid").**

   **option(PARTITIONPATH_FIELD_OPT_KEY, "partitionpath").**

   **option(TABLE_NAME, tableName).**

   **mode(Overwrite).**

   **save(basePath);**

   .. note::

      **"obs://testhudi/cow_table/"** is the OBS path, and **testhudi** is the name of the OBS parallel system file. Change them based on site requirements.

#. Use DataSource to check whether the table is created and whether the data is normal.

   **val roViewDF = spark.**

   **read.**

   **format("org.apache.hudi").**

   **load(basePath + "/*/*/*/*")**

   **roViewDF.createOrReplaceTempView("hudi_ro_table")**

   **spark.sql("select \* from hudi_ro_table").show()**

#. Run the **:q** command to exit the **spark-shell** CLI.

Configuring Ranger Permissions
------------------------------

#. Log in to FusionInsight Manager and choose **System** > **Permission** > **User Group**. On the displayed page, click **Create User Group**.

#. .. _mrs_01_248993__en-us_topic_0000001705304929_li55372842617:

   Create a user group without a role, for example, **obs_hudi**, and bind the user group to the corresponding user.

#. Log in to the Ranger management page as the **rangeradmin** user.

#. On the home page, click component plug-in name **OBS** in the **EXTERNAL AUTHORIZATION** area.

#. Click **Add New Policy** to add the **Read** and **Write** permissions on OBS paths to the user group created in :ref:`2 <mrs_01_248993__en-us_topic_0000001705304929_li55372842617>`. If there are no OBS paths, create one in advance (wildcard character **\*** is not allowed).

   |image1|

.. |image1| image:: /_static/images/en-us_image_0000001972894058.png
