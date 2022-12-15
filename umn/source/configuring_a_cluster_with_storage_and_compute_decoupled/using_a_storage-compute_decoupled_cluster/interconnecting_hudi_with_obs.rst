:original_name: mrs_01_24171.html

.. _mrs_01_24171:

Interconnecting Hudi with OBS
=============================

#. Log in to the client installation node as the client installation user.

#. Run the following commands to configure environment variables:

   **source ${client_home}/bigdata_env**

   **source ${client_home}/Hudi/component_env**

#. Modify the configuration file:

   **vim ${client_home}/Hudi/hudi/conf/hdfs-site.xml**

   .. code-block::

      <property>
      <name>dfs.namenode.acls.enabled</name>
      <value>false</value>
      </property>

#. For a security cluster, run the following command to perform user authentication. If Kerberos authentication is not enabled for the current cluster, you do not need to run this command.

   **kinit** *Username*

#. Start spark-shell and run the following commands to create a COW table and save it in OBS:

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

#. Use DataSource to check whether the table is successfully created and whether the data is normal.

   **val roViewDF = spark.**

   **read.**

   **format("org.apache.hudi").**

   **load(basePath + "/*/*/*/*")**

   **roViewDF.createOrReplaceTempView("hudi_ro_table")**

   **spark.sql("select \* from hudi_ro_table").show()**

#. Run the **:q** command to exit the spark-shell CLI.
