:original_name: mrs_01_0768.html

.. _mrs_01_0768:

Configuring a Storage-Compute Decoupled Cluster (Agency)
========================================================

MRS allows you to store data in OBS and use an MRS cluster for data computing only. In this way, storage and compute are separated. You can create an IAM agency, which enables ECS to automatically obtain the temporary AK/SK to access OBS. This prevents the AK/SK from being exposed in the configuration file.

By binding an agency, ECSs or BMSs can manage some of your resources. Determine whether to configure an agency based on the actual service scenario.

MRS provides the following configuration modes for accessing OBS. You can select one of them. The agency mode is recommended.

-  Bind an agency of the ECS type to an MRS cluster to access OBS, preventing the AK/SK from being exposed in the configuration file. For details, see the following part in this section.
-  Configure the AK/SK in an MRS cluster. The AK/SK will be exposed in the configuration file in plaintext. Exercise caution when performing this operation. For details, see :ref:`Configuring a Storage-Compute Decoupled Cluster (AK/SK) <mrs_01_0468>`.

This function is available for components Hadoop, Hive, Spark, Presto, and Flink in clusters of .

.. _mrs_01_0768__section092413322482:

(Optional) Step 1: Create an ECS Agency with OBS Access Permissions
-------------------------------------------------------------------

.. note::

   -  MRS presets **MRS_ECS_DEFAULT_AGENCY** in the agency list of IAM so that you can select this agency when creating a cluster. This agency has the **OBSOperateAccess** permission and the **CESFullAccess** (only available for users who have enabled fine-grained policies), **CES Administrator**, and **KMS Administrator** permissions in the region where the cluster is located. Do not modify **MRS_ECS_DEFAULT_AGENCY** on IAM.
   -  If you want to use the preset agency, skip the step for creating an agency. If you want to use a custom agency, perform the following steps to create an agency. (To create or modify an agency, you must have the Security Administrator permission.)

#. Log in to the management console.
#. Choose **Service List** > **Management & Governance** > **Identity and Access Management**.
#. Choose **Agencies**. On the displayed page, click **Create Agency**.
#. Enter an agency name, for example, **mrs_ecs_obs**.
#. Set **Agency Type** to **Cloud service** and select **ECS BMS** to authorize ECS or BMS to invoke OBS.
#. Set **Validity Period** to **Unlimited** and click **Next**.
#. On the displayed page, search for the **OBS OperateAccess** and select it.
#. Click **Next**. On the displayed page, select the desired scope for permissions you selected. By default, **All resources** is selected. Click **Show More** and select **Global resources**.
#. In the dialog box that is displayed, click **OK** to start authorization. After the message "**Authorization successful.**" is displayed, click **Finish**. The agency is successfully created.

Step 2: Create a Cluster with Storage and Compute Separated
-----------------------------------------------------------

You can configure an agency when creating a cluster or bind an agency to an existing cluster to separate storage and compute. This section uses a cluster with Kerberos authentication enabled as an example.

**Configuring an agency when creating a cluster**:

#. Log in to the MRS management console.

#. Click **Create Cluster**. The page for creating a cluster is displayed.

#. Click the **Custom Config** tab.

#. On the **Custom Config** tab page, set software parameters.

   -  **Region**: Select a region as required.
   -  **Cluster Name**: You can use the default name. However, you are advised to include a project name abbreviation or date for consolidated memory and easy distinguishing.
   -  **Cluster Version**: Select a cluster version.
   -  **Cluster Type**: Select **Analysis cluster** or **Hybrid cluster** and select all components.
   -  **Metadata**: Select **Local**.

#. Click **Next** and set hardware parameters.

   -  **AZ**: Use the default value.
   -  **VPC**: Use the default value.
   -  **Subnet**: Use the default value.
   -  **Security Group**: Use the default value.
   -  **EIP**: Use the default value.
   -  **Cluster Node**: Select the number of cluster nodes and node specifications based on site requirements.

#. Click **Next** and set related parameters.

   -  **Kerberos Authentication**: This function is enabled by default. You can enable or disable it.
   -  **Username**: The default username is **admin**, which is used to log in to MRS Manager.
   -  **Password**: Set a password for user **admin**.
   -  **Confirm Password**: Enter the password of user **admin** again.
   -  **Key Pair**: Select a key pair from the drop-down list to log in to an ECS. Select **"I acknowledge that I have obtained private key file** *SSHkey-xxx* **and that without this file I will not be able to log in to my ECS.**" If you have never created a key pair, click **View Key Pair** to create or import a key pair. And then, obtain a private key file.

#. In this example, configure an agency and leave other parameters blank. For details about how to configure other parameters, see :ref:`Advanced Options <mrs_01_0513__section1462335724114>`.

   **Agency**: Select the agency created in :ref:`(Optional) Step 1: Create an ECS Agency with OBS Access Permissions <mrs_01_0768__section092413322482>` or **MRS_ECS_DEFAULT_AGENCY** preset in IAM.

#. To enable secure communications, select **Enable**. For details, see :ref:`Communication Security Authorization <mrs_01_0786>`.

#. Click **Apply Now** and wait until the cluster is created.

   If Kerberos authentication is enabled for a cluster, check whether Kerberos authentication is required. If yes, click **Continue**. If no, click **Back** to disable Kerberos authentication and then create a cluster.

**Configuring an agency for an existing cluster**:

#. Log in to the MRS management console. In the left navigation pane, choose **Clusters** > **Active Clusters**.
#. Click the name of the cluster to enter its details page.
#. On the **Dashboard** page, click **Synchronize** on the right of **IAM User Sync** to synchronize IAM users.
#. On the **Dashboard** tab page, click **Manage Agency** on the right side of **Agency** to select an agency and click **OK** to bind it. Alternatively, click **Create Agency** to go to the IAM console to create an agency and select it.

Step 3: Create an OBS File System for Storing Data
--------------------------------------------------

.. note::

   In the big data decoupled storage-compute scenario, the OBS parallel file system must be used to configure a cluster. Using common object buckets will greatly affect the cluster performance.

#. Log in to OBS Console.

#. Choose **Parallel File System** > **Create Parallel File System**.

#. Enter the file system name, for example, **mrs-word001**.

   Set other parameters as required.

#. Click **Create Now**.

#. In the parallel file system list on the OBS console, click the file system name to go to the details page.

#. In the navigation pane, choose **Files** and create the **program** and **input** folders.

   -  **program**: Upload the program package to this folder.
   -  **input**: Upload the input data to this folder.

Step 4: Accessing the OBS File System
-------------------------------------

#. Log in to a Master node as user **root**. For details, see :ref:`Logging In to an ECS <mrs_01_0083>`.

#. Run the following command to set the environment variables:

   For versions earlier than MRS 3.x, run the **source /opt/client/bigdata_env** command.

   For MRS 3.x or later, run the **source /opt/Bigdata/client/bigdata_env** command.

#. Verify that Hadoop can access OBS.

   a. View the list of files in the file system **mrs-word001**.

      **hadoop fs -ls obs://mrs-word001/**

   b. Check whether the file list is returned. If it is returned, OBS access is successful.


      .. figure:: /_static/images/en-us_image_0000001296217708.png
         :alt: **Figure 1** Returned file list

         **Figure 1** Returned file list

#. Verify that Hive can access OBS.

   a. If Kerberos authentication has been enabled for the cluster, run the following command to authenticate the current user. The current user must have a permission to create Hive tables. For details about how to configure a role with a permission to create Hive tables, see :ref:`Creating a Role <mrs_01_0343>`. For details about how to create a user and bind a role to the user, see :ref:`Creating a User <mrs_01_0345>`. If Kerberos authentication is disabled for the current cluster, skip this step.

      **kinit** **MRS cluster user**

      Example: **kinit hiveuser**

   b. Run the client command of the Hive component.

      **beeline**

   c. Access the OBS directory in the beeline. For example, run the following command to create a Hive table and specify that data is stored in the **test_obs** directory of the file system **mrs-word001**:

      **create table test_obs(a int, b string) row format delimited fields terminated by "," stored as textfile location "obs://mrs-word001/test_obs";**

   d. Run the following command to query all tables. If table **test_obs** is displayed in the command output, OBS access is successful.

      **show tables;**


      .. figure:: /_static/images/en-us_image_0000001348738105.png
         :alt: **Figure 2** Returned table name

         **Figure 2** Returned table name

   e. Press **Ctrl+C** to exit the Hive beeline.

#. Verify that Spark can access OBS.

   a. Run the client command of the Spark component.

      **spark-beeline**

   b. Access OBS in spark-beeline. For example, create table **test** in the **obs://mrs-word001/table/** directory.

      **create table test(id int) location 'obs://mrs-word001/table/';**

   c. Run the following command to query all tables. If table **test** is displayed in the command output, OBS access is successful.

      **show tables;**


      .. figure:: /_static/images/en-us_image_0000001349057897.png
         :alt: **Figure 3** Returned table name

         **Figure 3** Returned table name

   d. Press **Ctrl+C** to exit the Spark beeline.

#. Verify that Presto can access OBS.

   -  For normal clusters with Kerberos authentication disabled

      a. Run the following command to connect to the client:

         **presto_cli.sh**

      b. On the Presto client, run the following statement to create a schema and set **location** to an OBS path:

         **CREATE SCHEMA hive.demo01 WITH (location = 'obs://mrs-word001/presto-demo002/');**

      c. Create a table in the schema. The table data is stored in the OBS file system. The following is an example.

         **CREATE TABLE hive.demo.demo_table WITH (format = 'ORC') AS SELECT \* FROM tpch.sf1.customer;**


         .. figure:: /_static/images/en-us_image_0000001349257377.png
            :alt: **Figure 4** Return result

            **Figure 4** Return result

      d. Run **exit** to exit the client.

   -  For security clusters with Kerberos authentication enabled

      a. .. _mrs_01_0768__li251015403210:

         Log in to MRS Manager and create a role with the Hive Admin Privilege permissions, for example, **prestorole**. For details about how to create a role, see :ref:`Creating a Role <mrs_01_0343>`.

      b. .. _mrs_01_0768__li55542531841:

         Create a user that belongs to the Presto and Hive groups and bind the role created in :ref:`6.a <mrs_01_0768__li251015403210>` to the user, for example, **presto001**. For details about how to create a user, see :ref:`Creating a User <mrs_01_0345>`.

      c. Authenticate the current user.

         **kinit presto001**

      d. Download the user credential.

         #. For MRS 3.x earlier, on MRS Manager, choose **System** > **Manage User**. In the row of the new user, choose **More** > **Download Authentication Credential**.


            .. figure:: /_static/images/en-us_image_0000001349057901.png
               :alt: **Figure 5** Downloading the Presto user authentication credential

               **Figure 5** Downloading the Presto user authentication credential

         #. On MRS Manager for MRS 3.x or later,, choose **System > Permission > User**. In the row that contains the newly added user, click **More > Download Authentication Credential**.


            .. figure:: /_static/images/en-us_image_0000001296058088.png
               :alt: **Figure 6** Downloading the Presto user authentication credential

               **Figure 6** Downloading the Presto user authentication credential

      e. .. _mrs_01_0768__li65281811161910:

         Decompress the downloaded user credential file, and save the obtained **krb5.conf** and **user.keytab** files to the client directory, for example, **/opt/Bigdata/client/Presto/**.

      f. .. _mrs_01_0768__li165280118198:

         Run the following command to obtain a user principal:

         **klist -kt /opt/Bigdata/client/Presto/user.keytab**

      g. For clusters with Kerberos authentication enabled, run the following command to connect to the Presto Server of the cluster:

         **presto_cli.sh --krb5-config-path {krb5.conf file path} --krb5-principal {user principal} --krb5-keytab-path {user.keytab file path} --user {presto username}**

         -  **krb5.conf** file path: Replace it with the file path set in :ref:`6.e <mrs_01_0768__li65281811161910>`, for example, **/opt/Bigdata/client/Presto/krb5.conf**.
         -  **user.keytab** file path: Replace it with the file path set in :ref:`6.e <mrs_01_0768__li65281811161910>`, for example, **/opt/Bigdata/client/Presto/user.keytab**.
         -  **user principal**: Replace it with the result returned in :ref:`6.f <mrs_01_0768__li165280118198>`.
         -  **presto username**: Replace it with the name of the user created in :ref:`6.b <mrs_01_0768__li55542531841>`, for example, **presto001**.

      h. On the Presto client, run the following statement to create a schema and set **location** to an OBS path:

         **CREATE SCHEMA hive.demo01 WITH (location = 'obs://mrs-word001/presto-demo002/');**

      i. Create a table in the schema. The table data is stored in the OBS file system. The following is an example.

         **CREATE TABLE hive.demo01.demo_table WITH (format = 'ORC') AS SELECT \* FROM tpch.sf1.customer;**


         .. figure:: /_static/images/en-us_image_0000001296058084.png
            :alt: **Figure 7** Return result

            **Figure 7** Return result

      j. Run **exit** to exit the client.

#. Verify that Flink can access OBS.

   a. On the **Dashboard** page, click **Synchronize** on the right of **IAM User Sync** to synchronize IAM users.

   b. After user synchronization is complete, choose **Jobs** > **Create** on the cluster details page to create a Flink job. In **Parameters**, enter parameters in **--input <Job input path> --output <Job output path>** format. You can click **OBS** to select a job input path, and enter a job output path that does not exist, for example, **obs://mrs-word001/output/**.

   c. On OBS Console, go to the output path specified during job creation. If the output directory is automatically created and contains the job execution results, OBS access is successful.


      .. figure:: /_static/images/en-us_image_0000001390874236.png
         :alt: **Figure 8** Flink job execution result

         **Figure 8** Flink job execution result

Reference
---------

For details about how to control permissions to access OBS, see :ref:`Configuring Fine-Grained Permissions for MRS Multi-User Access to OBS <mrs_01_0632>`.
