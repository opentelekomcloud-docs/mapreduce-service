:original_name: mrs_01_0407.html

.. _mrs_01_0407:

Preparing a Driver for MySQL Database Link
==========================================

Scenario
--------

As a component for batch data export, Loader can import and export data using a relational database.

Prerequisites
-------------

You have prepared service data.

Procedure
---------

**Procedure for MRS clusters earlier than 3.\ x:**

#. Download the MySQL JDBC driver **mysql-connector-java-5.1.21.jar** from the MySQL official website. For details about how to select the MySQL JDBC driver, see the following table.

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

#. Upload **mysql-connector-java-5.1.21.jar** to the Loader installation directory on the active and standby MRS Master nodes.

   -  For versions earlier than MRS 1.9.2, upload the package to **/opt/Bigdata/FusionInsight/FusionInsight-Sqoop-1.99.7/FusionInsight-Sqoop-1.99.7/server/jdbc**.

   -  For versions later than MRS 1.9.2 and earlier than MRS 3.x, upload the package to **/opt/Bigdata/MRS_XXX/install/FusionInsight-Sqoop-1.99.7/FusionInsight-Sqoop-1.99.7/server/jdbc/**.

      In the preceding path, **XXX** indicates the MRS version number. Change it based on site requirements.

#. Change the owner of the **mysql-connector-java-5.1.21.jar** package to **omm:wheel**.

#. Modify the **jdbc.properties** configuration file.

   Change the key value of **MYSQL** to **mysql-connector-java-5.1.21.jar**, for example, **MYSQL=mysql-connector-java-5.1.21.jar**.

#. Restart the Loader service.

**Procedure for MRS cluster 3.\ x and later versions:**

Modify the permission on the JAR package of the relational database driver.

#. Log in to the active and standby management nodes of the Loader service, obtain the driver JAR package of the relational database, and save it to the following directory on the active and standby Loader nodes: **${BIGDATA_HOME}/FusionInsight_Porter\_8.1.0.1/install/FusionInsight-Sqoop-1.99.3/FusionInsight-Sqoop-1.99.3/server/webapps/loader/WEB-INF/ext-lib**

   .. note::

      The version 8.1.0.1 is used as an example. Replace it with the actual version number.

#. Run the following commands as user **root** on the active and standby nodes of the Loader service to change the permission:

   **cd ${BIGDATA_HOME}/FusionInsight_Porter\_8.1.0.1/install/FusionInsight-Sqoop-1.99.3/FusionInsight-Sqoop-1.99.3/server/webapps/loader/WEB-INF/ext-lib**

   **chown omm:wheel** *JAR* *package name*

   **chmod 600** *JARpackage name*

#. Log in to FusionInsight Manager. Choose **Cluster** and click the target cluster name. In the navigation pane on the left, choose **Services** > **Loader**. In the upper right corner, choose **More**, select **Restart Service**, and enter the password of the administrator to restart the Loader service.
