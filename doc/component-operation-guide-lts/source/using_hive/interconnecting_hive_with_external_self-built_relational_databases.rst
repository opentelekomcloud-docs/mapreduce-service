:original_name: mrs_01_1751.html

.. _mrs_01_1751:

Interconnecting Hive with External Self-Built Relational Databases
==================================================================

.. note::

   -  This section describes how to connect Hive with built-in relational databases open-source MySQL and Postgres.
   -  After an external metadata database is deployed in a cluster with Hive data, the original metadata tables will not be automatically synchronized. Before installing Hive, determine whether to store metadata in an external database or DBService. For the former, deploy an external database when installing Hive or when there is no Hive data. After Hive installation, the metadata storage location cannot be changed. Otherwise, the original metadata will be lost.

**Hive supports access to open source MySQL and Postgres metabases.**

#. Install the open source MySQL or Postgres database.

   .. note::

      The node where the database is installed must be in the same network segment as the cluster, so that they can access each other.

#. Upload the driver package.

   -  PostgreSQL:

      Use the open source driver package to replace the cluster's existing one. Download the open source PostgreSQL driver package **postgresql-42.2.5.jar** at https://repo1.maven.org/maven2/org/postgresql/postgresql/42.2.5/ and upload it to the **${BIGDATA_HOME}/third_lib/Hive** directory on all MetaStore nodes.

      Run the following commands on all MetaStore nodes to modify the permission on the driver package:

      **cd ${BIGDATA_HOME}/third_lib/Hive**

      **chown omm:wheel** **postgresql-42.2.5.jar**

      **chmod 600** **postgresql-42.2.5.jar**

   -  MySQL:

      Visit the MySQL official website at https://www.mysql.com/, choose **DOWNLOADS** > **MySQL Community(GPL) DownLoads** > **Connector/J**, and download the driver package of the required version.

      -  Versions earlier than MRS 8.2.0, upload the driver package to the **/opt/Bigdata/FusionInsight_HD_*/install/FusionInsight-Hive-*/hive-*/lib/** directory on all RDSMetastore nodes.
      -  MRS 8.2.0 and later versions, upload the driver package to the **${BIGDATA_HOME}/third_lib/Hive** directory on all RDSMetastore nodes.

      Run the following commands on all MetaStore nodes to modify the permission on the driver package:

      **cd /opt/Bigdata/FusionInsight_HD_*/install/FusionInsight-Hive-*/hive-*/lib/**

      **chown omm:wheel** **mysql-connector-java-*.jar**

      **chmod 600** **mysql-connector-java-*.jar**

#. .. _mrs_01_1751__li1742162711619:

   Create a user and metadata database in the self-built database and assign all permissions on the database to the user. For example:

   -  Run the following commands in the PostgreSQL database to create the database **hivemeta** and the user **testuser**, and assign all permissions on **hivemeta** to **testuser**:

      **create user testuser with password 'password';**

      **create database hivemeta owner testuser;**

      **grant all privileges on database hivemeta to testuser;**

   -  Run the following commands in the MySQL database to create the database **hivemeta** and the user **testuser**, and assign all permissions on **hivemeta** to **testuser**:

      **create database hivemeta;**

      **create user 'testuser'@'%' identified by 'password';**

      **grant all privileges on hivemeta.\* to 'testuser';**

      **flush privileges;**

#. Import the SQL statements for creating metadata tables.

   -  SQL script path in the PostgreSQL database: **${BIGDATA_HOME}/FusionInsight_HD_*/install/FusionInsight-Hive-*/hive-*/scripts/metastore/upgrade/postgres/hive-schema-3.1.0.postgres.sql**

      Run the following command to import the SQL file to Postgres:

      **./bin/psql -U** *username* **-d** *databasename* **-f hive-schema-3.1.0.postgres.sql**

      Specifically:

      **./bin/psql** is in the Postgres installation directory.

      **username** indicates the username for logging in to Postgres.

      **databasename** indicates the database name.

   -  SQL script path in the MySQL database: **${BIGDATA_HOME}/FusionInsight_HD_*/install/FusionInsight-Hive-*/hive-*/scripts/metastore/upgrade/mysql/hive-schema-3.1.0.mysql.sql**

      Run the following command to import the SQL file to the MySQL database:

      **./bin/mysql -u** *username* **-p** *password* **-D** *databasename*\ **<hive-schema-3.1.0.mysql.sql**

      Specifically:

      **./bin/mysql** is in the MySQL installation directory.

      **username** indicates the user name for logging in to MySQL.

      **databasename** indicates the database name.

#. To connect Hive to the open source database, log in to FusionInsight Manager. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive**. Click **Configurations** then **All Configurations**, click **Hive(Service)**, select **MetaDB**, modify the following parameters, and click **Save**:

   .. table:: **Table 1** Parameters

      +---------------------------------------+-------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                             | Default Value                                                                                   | Description                                                                                                                                 |
      +=======================================+=================================================================================================+=============================================================================================================================================+
      | javax.jdo.option.ConnectionDriverName | org.postgresql.Driver                                                                           | Driver class for connecting metadata on MetaStore                                                                                           |
      |                                       |                                                                                                 |                                                                                                                                             |
      |                                       |                                                                                                 | -  If an external MySQL database is used, the value is:                                                                                     |
      |                                       |                                                                                                 |                                                                                                                                             |
      |                                       |                                                                                                 |    **com.mysql.jdbc.Driver**                                                                                                                |
      |                                       |                                                                                                 |                                                                                                                                             |
      |                                       |                                                                                                 | -  If an external Postgres database is used, the value is:                                                                                  |
      |                                       |                                                                                                 |                                                                                                                                             |
      |                                       |                                                                                                 |    **org.postgresql.Driver**                                                                                                                |
      +---------------------------------------+-------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
      | javax.jdo.option.ConnectionURL        | jdbc:postgresql://%{DBSERVICE_FLOAT_IP}%{DBServer}:%{DBSERVICE_CPORT}/hivemeta?socketTimeout=60 | URL of the JDBC link of the MetaStore metadata                                                                                              |
      |                                       |                                                                                                 |                                                                                                                                             |
      |                                       |                                                                                                 | -  If an external MySQL database is used, the value is:                                                                                     |
      |                                       |                                                                                                 |                                                                                                                                             |
      |                                       |                                                                                                 |    **jdbc:mysql://**\ *IP address of the MySQL database*\ **:**\ *Port number of the MySQL database*\ **/hivemeta?characterEncoding=utf-8** |
      |                                       |                                                                                                 |                                                                                                                                             |
      |                                       |                                                                                                 | -  If an external Postgres database is used, the value is:                                                                                  |
      |                                       |                                                                                                 |                                                                                                                                             |
      |                                       |                                                                                                 |    **jdbc:postgresql://**\ *IP address of the PostgreSQL database*\ **:**\ *Port number of the PostgreSQL database*\ **/hivemeta**          |
      +---------------------------------------+-------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
      | javax.jdo.option.ConnectionUserName   | hive${SERVICE_INDEX}${SERVICE_INDEX}                                                            | Username for connecting to the metadata database on Metastore                                                                               |
      +---------------------------------------+-------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+

#. Change the Postgres database password in MetaStore. Choose **Cluster** > **Name of the desired cluster** > **Services** > **Hive** > **Configurations** > **All Configurations** > **MetaStore(Role)** > **MetaDB**, modify the following parameters, and click **Save**.

   .. table:: **Table 2** Parameter

      +--------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------+
      | Parameter                                  | Default Value | Description                                                                                                               |
      +============================================+===============+===========================================================================================================================+
      | javax.jdo.option.extend.ConnectionPassword | \*****\*      | User password for connecting to the external metadata database on Metastore. The password is encrypted in the background. |
      +--------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------+

#. Log in to each MetaStore background node and check whether the local directory **/opt/Bigdata/tmp** exists.

   -  If yes, go to :ref:`8 <mrs_01_1751__li24241321154318>`.

   -  If no, run the following commands to create one:

      **mkdir -p /opt/Bigdata/tmp**

      **chmod 755 /opt/Bigdata/tmp**

#. .. _mrs_01_1751__li24241321154318:

   Save the configuration. Choose **Dashboard** > **More** > **Restart Service**, and enter the password to restart the Hive service.

#. Log in to the MySQL or PostgreSQL database and view metadata tables generated in the metadata database created in :ref:`3 <mrs_01_1751__li1742162711619>`.

   |image1|

#. Check whether the metadata database is successfully deployed.

   a. Log in to the node where the Hive client is installed as the client installation user.

      **cd** *Client installation directory*

      **source bigdata_env**

      **kinit** *Component service user* (Skip this step for clusters with Kerberos authentication disabled.)

   b. Run the following command to log in to the Hive client CLI:

      **beeline**

   c. Run the following command to create the **test** table:

      **create table** *test*\ **(id int,str1 string,str2 string);**

   d. Run the following command in the **hivemeta** database of the MySQL or PostgreSQL database to check whether there is any information about the **test** table:

      **select \* from TBLS;**

      If information about the **test** table is displayed, the external database is successfully deployed. For example:

      -  The result in the MySQL database is as follows:

         |image2|

      -  The result in the PostgreSQL database is as follows:

         |image3|

.. |image1| image:: /_static/images/en-us_image_0000001584077717.png
.. |image2| image:: /_static/images/en-us_image_0000001583757997.png
.. |image3| image:: /_static/images/en-us_image_0000001583957937.png
