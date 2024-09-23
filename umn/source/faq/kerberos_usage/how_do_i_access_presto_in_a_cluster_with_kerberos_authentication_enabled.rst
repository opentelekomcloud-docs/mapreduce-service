:original_name: mrs_03_1153.html

.. _mrs_03_1153:

How Do I Access Presto in a Cluster with Kerberos Authentication Enabled?
=========================================================================

#. Log in to the Master node in the cluster as user **root**.

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. Access Presto in a cluster with Kerberos authentication enabled.

   a. .. _mrs_03_1153__li251015403210:

      Log in to MRS Manager and create a role with the **Hive Admin Privilege** permission, for example, **prestorerole**.

   b. .. _mrs_03_1153__li55542531841:

      Create a user, for example, **presto001**, who belongs to the **Presto** and **Hive** groups, and bind the user to the role created in :ref:`3.a <mrs_03_1153__li251015403210>`.

   c. Authenticate user **presto001**.

      **kinit presto001**

   d. Download the user authentication credential.

      -  Operations on MRS Manager: Log in to MRS Manager and choose **System** > **Manage User**. Locate the row containing the new user, click **More**, and select **Download authentication credential**.

      -  Operations on MRS Manager:

         Log in to MRS Manager, choose **System** > **Permission** > **User**. On the displayed page, locate the row that contains the user, choose **More** > **Download Authentication Credential**.

   e. .. _mrs_03_1153__li65281811161910:

      Decompress the downloaded user credential file, and save the obtained **krb5.conf** and **user.keytab** files to the client directory, for example, /opt\ **/client/Presto/**.

   f. .. _mrs_03_1153__li165280118198:

      Run the following command to obtain the user principal:

      **klist -kt /opt/client/Presto/user.keytab**

   g. Run the following command to connect to the Presto Server of the cluster:

      **presto_cli.sh --krb5-config-path** *{krb5.conf file path}* **--krb5-principal** *{User's principal}* **--krb5-keytab-path** *{user.keytab file path}* **--user** *{presto username}*

      -  **krb5.conf** *file path*: file path set in :ref:`3.e <mrs_03_1153__li65281811161910>`, for example, **/opt/client/Presto/krb5.conf**.
      -  **user.keytab** *file path*: file path set in :ref:`3.e <mrs_03_1153__li65281811161910>`, for example, **/opt/client/Presto/user.keytab**.
      -  *User's principal*: principal obtained in :ref:`3.f <mrs_03_1153__li165280118198>`.
      -  *presto username*: user created in :ref:`3.b <mrs_03_1153__li55542531841>`, for example, **presto001**.

   h. On the Presto client, run the following statement to create a schema:

      **CREATE SCHEMA hive.demo01 WITH (location = 'obs://presto-demo002/');**

   i. Create a table in the schema. The table data is stored in the OBS bucket, as shown in the following example:

      **CREATE TABLE hive.demo01.demo_table WITH (format = 'ORC') AS SELECT \* FROM tpch.sf1.customer;**

   j. Run **exit** to exit the client.
