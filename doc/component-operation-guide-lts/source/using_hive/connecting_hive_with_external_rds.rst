:original_name: mrs_01_17511.html

.. _mrs_01_17511:

Connecting Hive with External RDS
=================================

.. note::

   -  RDS indicates the relational database in this section. This section describes how to connect Hive with the open-source MySQL and Postgres databases.
   -  After an external metadata database is deployed in a cluster with Hive data, the original metadata table will not be automatically synchronized. Therefore, before installing Hive, you need to check whether the metadata is external RDS or built-in DBService. If the metadata is external RDS, you need to configure the metadata to external RDS when installing Hive or when there is no Hive data. After the installation, the metadata cannot be modified. Otherwise, the original metadata will be lost.

**Hive supports access to open source MySQL and Postgres metabases.**

#. Install the open source MySQL or Postgres database.

   .. note::

      The node where the database is installed must be in the same network segment as the cluster, so that they can access each other.

#. Upload the driver package.

   -  Postgres: Use the open source Postgres driver package to replace the existing one of the cluster. Upload the Postgres driver package **postgresql-42.2.5.jar** to the *${BIGDATA_HOME}*\ **/third_lib/Hive** directory on all MetaStore instance nodes. To download the open-source driver package, visit https://repo1.maven.org/maven2/org/postgresql/postgresql/42.2.5/.
   -  MySQL: Go to the MySQL official website (https://www.mysql.com/), select **Downloads** > **Community** > **MySQL Connectors** > **Connector/J** to download the driver package of the corresponding version, and upload the driver package to the *${BIGDATA_HOME}*\ **/third_lib/Hive** directory on all RDSMetastore nodes.

#. Create a database in RDS as the specified database of Hive metadata.

   Run the following command in Postgres or MySQL:

   **create database** *databasename*\ **;**

   .. note::

      In the preceding command, *databasename* indicates the database name.

#. Import the SQL statements for creating metadata tables.

   -  Path of the Postgres SQL file: **${BIGDATA_HOME}/FusionInsight_HD\_8.1.2.2/install/FusionInsight-Hive-3.1.0/hive-3.1.0/scripts/metastore/upgrade/postgres/hive-schema-3.1.0.postgres.sql**

      Run the following command to import the SQL file to Postgres:

      **./bin/psql -U** *username* **-d** *databasename* **-f hive-schema-3.1.0.postgres.sql**

      Specifically:

      **./bin/psql** is in the Postgres installation directory.

      **username** indicates the username for logging in to Postgres.

      **databasename** indicates the database name.

   -  Path of the MySQL file: **${BIGDATA_HOME}/FusionInsight_HD\_8.1.2.2/install/FusionInsight-Hive-3.1.0/hive-3.1.0/scripts/metastore/upgrade/mysql/hive-schema-3.1.0.mysql.sql**

      Run the following command to import the SQL file to the MySQL database:

      **./bin/mysql -u** *username* **-p**\ *password* **-D**\ *databasename*\ **<hive-schema-3.1.0.mysql.sql**

      Specifically:

      **./bin/mysql** is in the MySQL installation directory.

      **username** indicates the user name for logging in to MySQL.

      **databasename** indicates the database name.

#. To connect Hive to the open-source database, log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Name of the desired cluster** > **Services** > **Hive** > **Configurations** > **All Configurations** > **Hive(Service)** > **MetaDB**, modify the following parameters, and click **Save**.

   .. table:: **Table 1** Parameter description

      +---------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
      | Parameter                             | Default Value                                                                                   | Description                                                                                |
      +=======================================+=================================================================================================+============================================================================================+
      | javax.jdo.option.ConnectionDriverName | org.postgresql.Driver                                                                           | Driver class for connecting metadata on MetaStore                                          |
      |                                       |                                                                                                 |                                                                                            |
      |                                       |                                                                                                 | -  If an external MySQL database is used, the value is:                                    |
      |                                       |                                                                                                 |                                                                                            |
      |                                       |                                                                                                 |    **com.mysql.jdbc.Driver**                                                               |
      |                                       |                                                                                                 |                                                                                            |
      |                                       |                                                                                                 | -  If an external Postgres database is used, the value is:                                 |
      |                                       |                                                                                                 |                                                                                            |
      |                                       |                                                                                                 |    **org.postgresql.Driver**                                                               |
      +---------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
      | javax.jdo.option.ConnectionURL        | jdbc:postgresql://%{DBSERVICE_FLOAT_IP}%{DBServer}:%{DBSERVICE_CPORT}/hivemeta?socketTimeout=60 | URL of the JDBC link of the MetaStore metadata                                             |
      |                                       |                                                                                                 |                                                                                            |
      |                                       |                                                                                                 | -  If an external MySQL database is used, the value is:                                    |
      |                                       |                                                                                                 |                                                                                            |
      |                                       |                                                                                                 |    **jdbc:mysql://**\ *MySQL IP address*:*MySQL port number*\ **/test? useSSL=false**      |
      |                                       |                                                                                                 |                                                                                            |
      |                                       |                                                                                                 | -  If an external Postgres database is used, the value is:                                 |
      |                                       |                                                                                                 |                                                                                            |
      |                                       |                                                                                                 |    **jdbc:postgresql://**\ *Postgres IP address*\ **:**\ *Postgres port number*\ **/test** |
      +---------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+
      | javax.jdo.option.ConnectionUserName   | hive${SERVICE_INDEX}${SERVICE_INDEX}                                                            | Username for connecting to the metadata database on Metastore                              |
      +---------------------------------------+-------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------+

#. Change the Postgres database password in MetaStore. Choose **Cluster** > **Name of the desired cluster** > **Services** > **Hive** > **Configurations** > **All Configurations** > **MetaStore(Role)** > **MetaDB**, modify the following parameters, and click **Save**.

   .. table:: **Table 2** Parameter description

      +--------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------+
      | Parameter                                  | Default Value | Description                                                                                                               |
      +============================================+===============+===========================================================================================================================+
      | javax.jdo.option.extend.ConnectionPassword | \*****\*      | User password for connecting to the external metadata database on Metastore. The password is encrypted in the background. |
      +--------------------------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------+

#. Log in to each MetaStore background node and check whether the local directory **/opt/Bigdata/tmp** exists.

   -  If yes, go to :ref:`8 <mrs_01_17511__en-us_topic_0000001219350615_li24241321154318>`.

   -  If no, run the following commands to create one:

      **mkdir -p /opt/Bigdata/tmp**

      **chmod 755 /opt/Bigdata/tmp**

#. .. _mrs_01_17511__en-us_topic_0000001219350615_li24241321154318:

   Save the configuration. Choose **Dashboard** > **More** > **Restart Service**, and enter the password to restart the Hive service.
