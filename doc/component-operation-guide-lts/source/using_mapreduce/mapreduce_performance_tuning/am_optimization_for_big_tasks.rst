:original_name: mrs_01_0847.html

.. _mrs_01_0847:

AM Optimization for Big Tasks
=============================

Scenario
--------

A big job containing 100,000 Map tasks fails. It is found that the failure is triggered by the slow response of ApplicationMaster (AM).

When the number of tasks increases, the number of objects managed by the AM increases, which requires much more memory for management. The default memory heap for AM is 1 GB.

Procedure
---------

You can improve the AM performance by setting the following parameters.

Navigation path for setting parameters:

Adjust the following parameters in the **mapred-site.xml** configuration file on the client to adjust the following parameters: The **mapred-site.xml** configuration file is in the **conf** directory of the client installation path, for example, **/opt/client/Yarn/config**.

+------------------------------------+-----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter                          | Description                                                                                                     | Default Value                                                                                                                                                                                                                  |
+====================================+=================================================================================================================+================================================================================================================================================================================================================================+
| yarn.app.mapreduce.am.resource.mb  | This parameter must be greater than the heap size specified by **yarn.app.mapreduce.am.command-opts**. Unit: MB | 1536                                                                                                                                                                                                                           |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| yarn.app.mapreduce.am.command-opts | Indicates the JVM startup parameters loaded to MapReduce ApplicationMaster.                                     | -Xmx1024m -XX:+UseConcMarkSweepGC -XX:+CMSParallelRemarkEnabled -verbose:gc -Djava.security.krb5.conf=${KRB5_CONFIG} -Dhadoop.home.dir=\ *${BIGDATA_HOME}*/FusionInsight_HD\_\ *xxx*/install/FusionInsight-Hadoop-*xxx*/hadoop |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
