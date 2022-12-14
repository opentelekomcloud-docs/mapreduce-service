:original_name: mrs_01_1999.html

.. _mrs_01_1999:

Optimizing SQL Query of Data of Multiple Sources
================================================

Scenario
--------

This section describes how to enable or disable the query optimization for inter-source complex SQL.

Procedure
---------

-  (Optional) Prepare for connecting to the MPPDB data source.

   If the data source to be connected is MPPDB, a class name conflict occurs because the MPPDB Driver file **gsjdbc4.jar** and the Spark JAR package **gsjdbc4-VXXXRXXXCXXSPCXXX.jar** contain the same class name. Therefore, before connecting to the MPPDB data source, perform the following steps:

   #. Move **gsjdbc4-VXXXRXXXCXXSPCXXX.jar** from Spark. Spark running does not depend on this JAR file. Therefore, moving this JAR file to another directory (for example, the **/tmp** directory) will not affect Spark running.

      a. Log in to the Spark server and move **gsjdbc4-VXXXRXXXCXXSPCXXX.jar** from the **${BIGDATA_HOME}/FusionInsight_Spark2x\_8.1.0.1/install/FusionInsight-Spark2x-3.1.1/spark/jars** directory.
      b. Log in to the Spark client host and move **gsjdbc4-VXXXRXXXCXXSPCXXX.jar** from the **/opt/client/Spark2x/spark/jars** directory.

   #. Obtain the MPPDB Driver file **gsjdbc4.jar** from the MPPDB installation package and upload the file to the following directories:

      .. note::

         Obtain **gsjdbc4.jar** from **FusionInsight_MPPDB\\software\\components\\package\\FusionInsight-MPPDB-**\ *xxx*\ **\\package\\Gauss-MPPDB-ALL-PACKAGES\\GaussDB-**\ *xxx*\ **-REDHAT-**\ *xxx*\ **-Jdbc\\jdbc**, the directory where the MPPDB installation package is stored.

      -  **/${BIGDATA_HOME}/FusionInsight_Spark2x\_8.1.0.1/install/FusionInsight-Spark2x-3.1.1/spark/jars** on the Spark server.
      -  **/opt/client/Spark2x/spark/jars** on the Spark client.

   #. Update the **/user/spark2x/jars/8.1.0.1/spark-archive-2x.zip** package stored in the HDFS.

      .. note::

         The version 8.1.0.1 is used as an example. Replace it with the actual version number.

      a. Log in to the node where the client is installed as a client installation user. Run the following command to switch to the client installation directory, for example, **/opt/client**:

         **cd /opt/client**

      b. Run the following command to configure environment variables:

         **source bigdata_env**

      c. If the cluster is in security mode, run the following command to get authenticated:

         **kinit** *Component service user*

      d. Run the following commands to create the temporary file **./tmp**, obtain **spark-archive-2x.zip** from HDFS, and decompress it to the **tmp** directory:

         **mkdir tmp**

         **hdfs dfs -get** /user/spark2x/jars/8.1.0.1/spark-archive-2x.zip **./**

         **unzip spark-archive-2x.zip -d ./tmp**

      e. .. _mrs_01_1999__lc86ecd4e025841f89961e2125940d316:

         Switch to the **tmp** directory, delete the **gsjdbc4-VXXXRXXXCXXSPCXXX.jar** file, upload the MPPDB Driver file **gsjdbc4.jar** to the **tmp** directory, and run the following command to compress the file again:

         **zip -r spark-archive-2x.zip \*.jar**

      f. Delete **spark-archive-2x.zip** from the HDFS and update the **spark-archive-2x.zip** package generated in :ref:`3.e <mrs_01_1999__lc86ecd4e025841f89961e2125940d316>` to the **/user/spark2x/jars/8.1.0.1/** directory in the HDFS.

         **hdfs dfs -rm** /user/spark2x/jars/8.1.0.1/spark-archive-2x.zip

         **hdfs dfs -put** ./spark-archive-2x.zip /user/spark2x/jars/8.1.0.1

   #. Restart the Spark service. After the Spark service is restarted, restart the Spark client.

-  Enable the optimization function.

   For all modules that support query pushdown, you can run the **SET** command on the **spark-beeline** client to enable the cross-source query optimization function. By default, the function is disabled.

   Pushdown configurations can be performed in dimensions of global, data sources, and tables. Commands are as follows:

   -  Global (valid for all data sources):

      **SET spark.sql.datasource.jdbc = project,aggregate,orderby-limit**

   -  Data sources:

      **SET spark.sql.datasource.${url} = project,aggregate,orderby-limit**

   -  Tables:

      **SET spark.sql.datasource.${url}.${table} = project,aggregate,orderby-limit**

   When you run the **SET** command to configure preceding parameters, you are allowed to specify multiple pushdown modules and separate them by commas. The following table lists parameters of corresponding pushdown modules.

   .. table:: **Table 1** Parameters of modules

      +-------------------------------------------+------------------------------------+
      | Module                                    | Parameter Value in the SET Command |
      +===========================================+====================================+
      | project                                   | project                            |
      +-------------------------------------------+------------------------------------+
      | aggregate                                 | aggregate                          |
      +-------------------------------------------+------------------------------------+
      | order by, limit over project or aggregate | orderby-limit                      |
      +-------------------------------------------+------------------------------------+

   The following is a statement for creating an external table of MySQL:

   **create table if not exists pdmysql using org.apache.spark.sql.jdbc options(driver "com.mysql.jdbc.Driver", url "jdbc:mysql://ip2:3306/test", user "hive", password "*xxx*", dbtable "mysqldata");**

   In the preceding statement:

   -  ${url} = jdbc:mysql://ip2:3306/test
   -  ${table} = mysqldata

   .. note::

      -  On the right of the equal sign (=) is the operators (separated by commas) to be enabled by pushdown.
      -  Priority: table > data source > global. If the table switch is set, the global switch of the data source is invalid for the table. If a data source switch is set, the global switch is invalid for the data source.
      -  The equal sign (=) is not allowed in URL. Equal signs (=) are automatically deleted in the SET clause.
      -  After multiple SET operations, results with different keys will not overwrite each other.

-  Add functions that support query pushdown.

   In addition to query pushdown of mathematical, time, and string functions such as abs(), month(), and length(), you can run the **SET** command to add a data source that supports query pushdown. Run the following command on the Spark-beeline client:

   **SET spark.sql.datasource.${datasource}.functions = fun1,fun2**

-  Reset the configuration set by the **SET** command.

   Currently, you can only run the **RESET** command on the **spark-beeline** client to cancel all **SET** content. After running the **RESET** command, all values in the **SET** command will be cleared. Exercise caution when performing this operation.

   The **SET** command is valid in the current session on the client. After the client is shut down, the content in the **SET** command turns invalid.

   Alternatively, change the value of **spark.sql.locale.support** in the **spark-defaults.conf** file to **true**.

Precautions
-----------

Only MySQL, MPPDB, Hive, oracle, and PostgreSQL data sources are supported.
