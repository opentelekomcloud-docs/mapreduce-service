:original_name: mrs_01_1469.html

.. _mrs_01_1469:

How Do I Logically Split Data Across Different Namespaces?
==========================================================

Question
--------

How do I logically split data across different namespaces?

Answer
------

-  Configuration:

   To logically split data across different namespaces, you must update the following configuration in the **core-site.xml** file of HDFS, Hive, and Spark.

   .. note::

      Changing the Hive component will change the locations of carbonstore and warehouse.

   -  Configuration in HDFS

      -  **fs.defaultFS**: Name of the default file system. The URI mode must be set to **viewfs**. When **viewfs** is used, the permission part must be **ClusterX**.
      -  **fs.viewfs.mountable.ClusterX.homedir**: Home directory base path. You can use the getHomeDirectory() method defined in **FileSystem/FileContext** to access the home directory.
      -  fs.viewfs.mountable.default.link.<dir_name>: ViewFS mount table.

      Example:

      .. code-block::

         <property>
         <name>fs.defaultFS</name>
         <value>viewfs://ClusterX/</value>
         </property>
         <property>
         <name>fs.viewfs.mounttable.ClusterX.link./folder1</name>
         <value>hdfs://NS1/folder1</value>
         </property>
         <property>
         <name>fs.viewfs.mounttable.ClusterX.link./folder2</name>
         <value>hdfs://NS2/folder2</value>
         </property>

   -  Configurations in Hive and Spark

      **fs.defaultFS**: Name of the default file system. The URI mode must be set to **viewfs**. When **viewfs** is used, the permission part must be **ClusterX**.

-  Syntax:

   **LOAD DATA INPATH** *'path to data' INTO TABLE table_name OPTIONS ``('...');``*

   .. note::

      When Spark is configured with the viewFS file system and attempts to load data from HDFS, users must specify a path such as **viewfs://** or a relative path as the file path in the **LOAD** statement.

-  Example:

   -  Sample viewFS path:

      **LOAD DATA INPATH** *'viewfs://ClusterX/dir/data.csv' INTO TABLE table_name OPTIONS ``('...');``*

   -  Sample relative path:

      **LOAD DATA INPATH** *'/apps/input_data1.txt'* **INTO TABLE** *table_name*;
