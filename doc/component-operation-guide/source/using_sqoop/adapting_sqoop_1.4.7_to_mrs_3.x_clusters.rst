:original_name: mrs_01_24455.html

.. _mrs_01_24455:

Adapting Sqoop 1.4.7 to MRS 3.\ *x* Clusters
============================================

Sqoop is a tool designed for efficiently transmitting a large amount of data between Apache Hadoop and structured databases (such as relational databases). Customers need to use Sqoop to migrate data in MRS. However, MRS of an earlier version does not provide Sqoop. This section describes how to install and use Sqoop. In MRS 3.1.0 or later, you can select the Sqoop component during cluster creation.

Prerequisites
-------------

The MRS client and the JDK environment have been installed.

|image1|

Procedure
---------

#. `Download <http://archive.apache.org/dist/sqoop/1.4.7/>`__ the open-source **sqoop-1.4.7.bin__hadoop-2.6.0.tar.gz** package.

#. Save the downloaded package to the **/opt/Bigdata/client** directory on the node where the MRS client is installed and decompress it.

   **tar zxvf sqoop-1.4.7.bin__hadoop-2.6.0.tar.gz**

#. Download the MySQL JDBC driver **mysql-connector-java-xxx.jar** from the MySQL official website. For details about how to select the MySQL JDBC driver, see the following table.

   .. table:: **Table 1** Version information

      +---------------------+---------------------------------------------------------------------------------+
      | JDBC Driver Version | MySQL Version                                                                   |
      +=====================+=================================================================================+
      | Connector/J 5.1     | MySQL 4.1, MySQL 5.0, MySQL 5.1, and MySQL 6.0 alpha                            |
      +---------------------+---------------------------------------------------------------------------------+
      | Connector/J 5.0     | MySQL 4.1, MySQL 5.0 servers, and distributed transaction (XA)                  |
      +---------------------+---------------------------------------------------------------------------------+
      | Connector/J 3.1     | MySQL 4.1, MySQL 5.0 servers, and MySQL 5.0 except distributed transaction (XA) |
      +---------------------+---------------------------------------------------------------------------------+
      | Connector/J 3.0     | MySQL 3.x and MySQL 4.1                                                         |
      +---------------------+---------------------------------------------------------------------------------+

#. Put the MySQL driver package in the **/opt/Bigdata/client/sqoop-1.4.7.bin__hadoop-2.6.0/lib** directory of Sqoop and modify the owner group and permission of the JAR package. For details, see the owner group and permission of **omm:wheel** and **755** in :ref:`Figure 1 <mrs_01_24455__fig71925061212>`.

   .. _mrs_01_24455__fig71925061212:

   .. figure:: /_static/images/en-us_image_0000001295770408.png
      :alt: **Figure 1** Owner group and permission of the MySQL driver package

      **Figure 1** Owner group and permission of the MySQL driver package

#. Replace the JAR package in the **lib** directory of Sqoop with that starting with **jackson** in the **lib** directory of Hive on the MRS client, for example, **/opt/Bigdata/client/Hive/Beeline/lib**.


   .. figure:: /_static/images/en-us_image_0000001349090041.png
      :alt: **Figure 2** JAR package starting with **jackson**

      **Figure 2** JAR package starting with **jackson**

#. Copy the **jline** package from the **/opt/Bigdata/client/Hive/Beeline/lib** directory of the MRS Hive client to the **lib** directory of Sqoop.

#. Run the **vim $JAVA_HOME/jre/lib/security/java.policy** command to add the following configuration:

   **permission javax.management.MBeanTrustPermission "register";**

#. Run the following commands to go to the **conf** directory of the Sqoop and add the configuration items of variables:

   **cd /opt/Bigdata/client/sqoop-1.4.7.bin__hadoop-2.6.0/conf**

   **cp sqoop-env-template.sh sqoop-env.sh**

#. Run the **vim sqoop-env.sh** command to set the environment variables of Sqoop. Change the Hadoop and Hive directories as required.

   .. code-block::

      export HADOOP_COMMON_HOME=/opt/Bigdata/client/HDFS/hadoop
      export HADOOP_MAPRED_HOME=/opt/Bigdata/client/HDFS/hadoop
      export HIVE_HOME=/opt/Bigdata/MRS_1.9.X/install/FusionInsight-Hive-3.1.0/hive (Enter the actual path.)
      export HIVE_CONF_DIR=/opt/Bigdata/client/Hive/config
      export HCAT_HOME=/opt/Bigdata/client/Hive/HCatalog


   .. figure:: /_static/images/en-us_image_0000001438712537.png
      :alt: **Figure 3** Setting environment variables of Sqoop

      **Figure 3** Setting environment variables of Sqoop

#. Build the sqoop script. For example:

   .. code-block::

      /opt/Bigdata/FusionInsight_Current/1_19_SqoopClient/install/FusionInsight-Sqoop-1.4.7/bin/sqoop import
      --connect jdbc:mysql://192.168.0.183:3306/test
      --driver com.mysql.jdbc.Driver
      --username 'root'
      --password 'xxx'
      --query "SELECT id, name  FROM tbtest WHERE \$CONDITIONS"
      --hcatalog-database default
      --hcatalog-table test
      --num-mappers 1

.. |image1| image:: /_static/images/en-us_image_0000001295930368.png
