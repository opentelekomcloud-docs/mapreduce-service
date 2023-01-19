:original_name: mrs_01_1944.html

.. _mrs_01_1944:

Configuring the Switchover Between the Multi-active Instance Mode and the Multi-tenant Mode
===========================================================================================

Scenarios
---------

When using a cluster, if you want to switch between multi-active instance mode and multi-tenant mode, the following configurations are required.

-  Switch from multi-tenant mode to multi-active instance mode.

   Modify the following parameters of the Spark2x service:

   -  spark.thriftserver.proxy.enabled=false
   -  spark.scheduler.allocation.file=#{conf_dir}/fairscheduler.xml
   -  spark.proxyserver.hash.enabled=false

-  Switch from multi-active instance mode to multi-tenant mode.

   Modify the following parameters of the Spark2x service:

   -  spark.thriftserver.proxy.enabled=true
   -  spark.scheduler.allocation.file=./__spark_conf__/__hadoop_conf__/fairscheduler.xml
   -  spark.proxyserver.hash.enabled=true

Configuration Description
-------------------------

Log in to Manager, choose **Cluster** > *Name of the desired cluster* > **Service** > **Spark2x** > **Configuration**, click **All Configurations**, and search for and modify the following parameters.

.. table:: **Table 1** Parameter description

   +---------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
   | Parameter                       | Description                                                                                                                    | Default Value                                                               |
   +=================================+================================================================================================================================+=============================================================================+
   | spark.scheduler.allocation.file | Specifies the fair scheduling file path.                                                                                       | ./__spark_conf__/__hadoop_conf__/fairscheduler.xml                          |
   |                                 |                                                                                                                                |                                                                             |
   |                                 | -  If the multi-active instance mode is used, the path is changed to **#{conf_dir}/fairscheduler.xml**.                        |                                                                             |
   |                                 | -  If multi-tenant mode is used, the path is changed to **./__spark_conf__/__hadoop_conf__/fairscheduler.xml**.                |                                                                             |
   +---------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
   | spark.proxyserver.hash.enabled  | Specifies whether to connect to ProxyServer using the Hash algorithm.                                                          | true                                                                        |
   |                                 |                                                                                                                                |                                                                             |
   |                                 | -  **true** indicates using the Hash algorithm. In multi-tenant mode, this parameter must be configured to **true**.           | .. note::                                                                   |
   |                                 | -  **false** indicates using random connection. In multi-active instance mode, this parameter must be configured to **false**. |                                                                             |
   |                                 |                                                                                                                                |    After this parameter is modified, you need to download the client again. |
   +---------------------------------+--------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
