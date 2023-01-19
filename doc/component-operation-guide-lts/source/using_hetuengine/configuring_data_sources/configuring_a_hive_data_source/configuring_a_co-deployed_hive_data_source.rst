:original_name: mrs_01_24253.html

.. _mrs_01_24253:

Configuring a Co-deployed Hive Data Source
==========================================

Scenario
--------

This section describes how to add a Hive data source of the same Hadoop cluster as HetuEngine on HSConsole.

Currently, HetuEngine supports data sources of the following traditional data formats: AVRO, TEXT, RCTEXT, Binary, ORC, Parquet, and SequenceFile.

Prerequisites
-------------

A HetuEngine compute instance has been created.

.. note::

   The HetuEngine service is interconnected to its co-deployed Hive data source by default during its installation. The data source name is **hive** and cannot be deleted. Some default configurations cannot be modified. You need to restart the HetuEngine service to automatically synchronize these unmodifiable configurations once they are updated.

Procedure
---------

#. Log in to FusionInsight Manager as a HetuEngine administrator and choose **Cluster** > **Services** > **HetuEngine**.
#. In the **Basic Information** area on the **Dashboard** page, click the link next to **HSConsole WebUI**.
#. On HSConsole, choose **Data Source**. Locate the row that contains the target Hive data source, click **Edit** in the **Operation** column, and modify the configurations. The following table describes data source configurations that can be modified.

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                        | Example Value                                         |
   +===================================+====================================================================================================================================================================+=======================================================+
   | Description                       | Description of the data source.                                                                                                                                    | ``-``                                                 |
   |                                   |                                                                                                                                                                    |                                                       |
   |                                   | The value can contain only letters, digits, commas (,), periods (.), underscores (_), spaces, and line breaks.                                                     |                                                       |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------+
   | Enable Data Source Authentication | Whether to use the permission policy of the Hive data source for authentication.                                                                                   | No                                                    |
   |                                   |                                                                                                                                                                    |                                                       |
   |                                   | If Ranger is disabled for the HetuEngine service, select **Yes**. If Ranger is enabled, select **No**.                                                             |                                                       |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------+
   | Metastore URL                     | Value of **hive.metastore.uris** in **hive-site.xml** on the data source client. When the Hive MetaStore instance changes, you need to manually update this value. | thrift://192.168.1.1:21088,thrift://192.168.1.2:21088 |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------+
   | Enable Connection Pool            | Whether to enable the connection pool when accessing Hive MetaStore. The default value is **Yes**                                                                  | Yes                                                   |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------+
   | Maximum Connections               | Maximum number of connections in the connection pool when accessing Hive MetaStore.                                                                                | 50 (Value range: 0-200)                               |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------+

#. (Optional) If you need to add **Custom Configuration**, complete the configurations by referring to :ref:`6.g <mrs_01_2348__en-us_topic_0000001219351171_li1438274211549>` and click **OK** to save the configurations.
