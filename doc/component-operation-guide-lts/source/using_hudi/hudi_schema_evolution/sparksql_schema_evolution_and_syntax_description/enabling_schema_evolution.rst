:original_name: mrs_01_24496.html

.. _mrs_01_24496:

Enabling Schema Evolution
=========================

.. caution::

   Schema evolution cannot be disabled once being enabled.

-  To use spark-beeline, log in to FusionInsight Manager, choose **Cluster** > **Services** > **Spark2x**, and click the **Configurations** tab then the **All Configurations** sub-tab.

   Search for **spark.sql.extensions** in the search box and change its value of JDBCServer to **org.apache.spark.sql.hive.FISparkSessionExtension,org.apache.spark.sql.hudi.HoodieSparkSessionExtension,org.apache.spark.sql.hive.CarbonInternalExtensions**.

-  For SQL operations, run the following command before running any SQL statements:

   .. code-block::

      set hoodie.schema.evolution.enable=true

-  For API calls, specify the following parameter in DataFrame options:

   .. code-block::

      hoodie.schema.evolution.enable -> true
