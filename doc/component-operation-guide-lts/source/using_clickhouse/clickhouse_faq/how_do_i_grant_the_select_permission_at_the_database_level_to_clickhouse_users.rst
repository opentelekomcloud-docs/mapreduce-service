:original_name: mrs_01_24846.html

.. _mrs_01_24846:

How Do I Grant the Select Permission at the Database Level to ClickHouse Users?
===============================================================================

Procedure
---------

#. Log in to the node where the ClickHouse client is installed in the MRS cluster and run the following commands:

   **su - omm**

   **source** *{Client installation directory}*\ **/bigdata_env**

   **kinit** *Component user* (You do not need to run the **kinit** command for normal clusters.)

   **clickhouse client --host** *IP address of the ClickHouse node* **--port 9000 -m --user clickhouse -password '**\ *Password of the ClickHouse user*\ **'**

   .. note::

      View the password of the ClickHouse user.

      Log in to FusionInsight Manager and choose **Cluster** > **Services** > **ClickHouse**. Click **Instance** and click any ClickHouseServer role name. Go to the **Dashboard** tab page of ClickHouseServer, click the **users.xml** file in **Configuration File** area, and view the password of the ClickHouse user.

#. You can use either of the following methods to create a role with the read-only permission for a specified database:

   Method 1

   a. Creating a role with the read-only permission for a specified database (the **default** database is used as an example)

      **create role ck_role on cluster default_cluster;**

      **GRANT SELECT ON default.\* TO ck_role on cluster default_cluster;**

   b. Creating a common user

      **CREATE USER user_01 on cluster default_cluster IDENTIFIED WITH PLAINTEXT_PASSWORD BY 'password';**

   c. Granting the read-only permission role to a common user

      **GRANT ck_role to user_01 on cluster default_cluster;**

   d. Viewing user permissions

      **show grants for user_01;**

      **select \* from system.grants where role_name = 'ck_role';**

   Method 2

   Creating a user with the read-only permission for a specified database

   a. Creating a user:

      **CREATE USER user_01 on cluster default_cluster IDENTIFIED WITH PLAINTEXT_PASSWORD BY 'password';**

   b. Granting the query permission on a specified database to the created user:

      **grant select on default.\* to user_01 on cluster default_cluster;**

   c. Querying user permissions:

      **select \* from system.grants where user_name = 'user_01';**
