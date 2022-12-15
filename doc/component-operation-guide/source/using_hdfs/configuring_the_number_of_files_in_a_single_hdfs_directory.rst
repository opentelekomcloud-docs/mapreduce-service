:original_name: mrs_01_0805.html

.. _mrs_01_0805:

Configuring the Number of Files in a Single HDFS Directory
==========================================================

Scenario
--------

Generally, multiple services are deployed in a cluster, and the storage of most services depends on the HDFS file system. Different components such as Spark and Yarn or clients are constantly writing files to the same HDFS directory when the cluster is running. However, the number of files in a single directory in HDFS is limited. Users must plan to prevent excessive files in a single directory and task failure.

You can set the number of files in a single directory using the **dfs.namenode.fs-limits.max-directory-items** parameter in HDFS.

Procedure
---------

#. Go to the **All Configurations** page of HDFS by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.
#. Search for the configuration item **dfs.namenode.fs-limits.max-directory-items**.

   .. table:: **Table 1** Parameter description

      +--------------------------------------------+----------------------------------------+-----------------------+
      | Parameter                                  | Description                            | Default Value         |
      +============================================+========================================+=======================+
      | dfs.namenode.fs-limits.max-directory-items | Maximum number of items in a directory | 1048576               |
      |                                            |                                        |                       |
      |                                            | Value range: 1 to 6,400,000            |                       |
      +--------------------------------------------+----------------------------------------+-----------------------+

#. Set the maximum number of files that can be stored in a single HDFS directory. Save the modified configuration. Restart the expired service or instance for the configuration to take effect.

   .. note::

      Plan data storage in advance based on time and service type categories to prevent excessive files in a single directory. You are advised to use the default value, which is about 1 million pieces of data in a single directory.
