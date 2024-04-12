:original_name: mrs_01_24237.html

.. _mrs_01_24237:

Uploading a Driver File
=======================

Scenario
--------

CDL is a simple and efficient real-time data integration service. It captures events from various OLTP databases and pushes them to Kafka. When creating a database connection on the CDLService Web UI, you can upload the database's driver file to the Web UI for unified management.

Prerequisites
-------------

-  You have obtained the driver JAR package of the database to be connected. The driver JAR package of the MySQL database is **mysql-connector-java-8.0.24.jar**.
-  Drivers need to be uploaded only for the MySQL data sources.
-  A user with the CDL management permission has been created for the cluster with Kerberos authentication enabled.

Procedure
---------

#. Access the CDLService web UI as a user with the CDL management permissions or the **admin** user (for the cluster where Kerberos authentication is not enabled). For details, see :ref:`Logging In to the CDLService WebUI <mrs_01_24236>`.
#. Choose **Driver Management** and click **Upload Driver**. In the displayed dialog box, select the prepared database driver file and click **Open**.
#. On the **Driver Management** page, check whether the list of driver file names is displayed properly.

   .. note::

      -  If a driver is no longer used or is mistakenly uploaded, click **Delete** to delete its driver file.
      -  If there are a large number of driver files, you can enter a driver file name in the search box to quickly search for the desired driver file.
