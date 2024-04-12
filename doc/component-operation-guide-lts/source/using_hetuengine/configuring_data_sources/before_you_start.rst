:original_name: mrs_01_2315.html

.. _mrs_01_2315:

Before You Start
================

HetuEngine supports quick joint query of multiple data sources and GUI-based data source configuration and management. You can quickly add a data source on the HSConsole page.

:ref:`Table 1 <mrs_01_2315__en-us_topic_0000001173789582_table667372634317>` lists the data sources supported by HetuEngine of the current version.

.. _mrs_01_2315__en-us_topic_0000001173789582_table667372634317:

.. table:: **Table 1** List for connecting HetuEngine to data sources

   +-----------------+---------------+------------------+---------------------------------------------------------------+
   | HetuEngine Mode | Data Source   | Data Source Mode | Supported Data Source Version                                 |
   +=================+===============+==================+===============================================================+
   | Security mode   | Hive          | Security mode    | MRS 3.x, FusionInsight 6.5.1, and Hive in the current cluster |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   |                 | HBase         |                  | MRS 3.x and FusionInsight 6.5.1                               |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   |                 | Elasticsearch |                  | Elasticsearch of the current cluster                          |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   |                 | HetuEngine    |                  | MRS 3.x                                                       |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   |                 | GaussDB       |                  | GaussDB 200 and GaussDB A 8.0.0                               |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   |                 | Hudi          |                  | MRS 3.1.2 or later                                            |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   |                 | ClickHouse    |                  | MRS 3.1.1 or later                                            |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   | Normal mode     | Hive          | Normal mode      | MRS 3.x, FusionInsight 6.5.1, and Hive in the current cluster |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   |                 | HBase         |                  | MRS 3.x and FusionInsight 6.5.1                               |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   |                 | Elasticsearch |                  | Elasticsearch of the current cluster                          |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   |                 | Hudi          |                  | MRS 3.1.2 or later                                            |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   |                 | ClickHouse    |                  | MRS 3.1.1 or later                                            |
   +-----------------+---------------+------------------+---------------------------------------------------------------+
   |                 | GaussDB       | Security mode    | GaussDB 200 and GaussDB A 8.0.0                               |
   +-----------------+---------------+------------------+---------------------------------------------------------------+

Operations such as adding, configuring, and deleting a HetuEngine data source takes effect dynamically without restarting the cluster.

A configured data source takes effect dynamically and you cannot disable this function. By default, the interval for a data source to dynamically take effect is 60 seconds. You can change the interval to a desired one by changing the value of **catalog.scanner-interval** in **coordinator.config.properties** and **worker.config.properties** by referring to :ref:`3.e <mrs_01_1731__en-us_topic_0000001173631202_li135621231135216>` in :ref:`Creating HetuEngine Compute Instances <mrs_01_1731>`. See the following example.

.. code-block::

   catalog.scanner-interval =120s

.. note::

   -  The domain name of the data source cluster must be different from that of the HetuEngine cluster. In addition, two data sources with the same domain name cannot be connected to at the same time.
   -  The data source cluster and the HetuEngine cluster can communicate with each other.
