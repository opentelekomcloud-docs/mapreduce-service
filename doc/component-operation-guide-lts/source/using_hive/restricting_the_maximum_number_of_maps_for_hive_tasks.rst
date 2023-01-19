:original_name: mrs_01_0973.html

.. _mrs_01_0973:

Restricting the Maximum Number of Maps for Hive Tasks
=====================================================

Scenario
--------

-  This function applies to Hive.
-  This function is used to limit the maximum number of maps for Hive tasks on the server to avoid performance deterioration caused by overload of the HiveSever service.

Procedure
---------

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **Hive** > **Configurations** > **All Configurations**.
#. Choose **MetaStore(Role)** > **Customization**, add a customized parameter to the **hivemetastore-site.xml** parameter file, set **Name** to **hive.mapreduce.per.task.max.splits**, and set the parameter to a large value. Restart all Hive instances after the modification.
