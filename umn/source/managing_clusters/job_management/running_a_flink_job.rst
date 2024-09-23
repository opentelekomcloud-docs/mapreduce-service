:original_name: mrs_01_0527.html

.. _mrs_01_0527:

Running a Flink Job
===================

You can submit programs developed by yourself to MRS to execute them, and obtain the results. This section describes how to submit a Flink job on the MRS management console. Flink jobs are used to submit JAR programs to process streaming data.

Prerequisites
-------------

You have uploaded the program packages and data files required for running jobs to OBS or HDFS.

Submitting a Job on the GUI
---------------------------

#. Log in to the MRS console.

#. Choose **Clusters > Active Clusters**, select a running cluster, and click its name to switch to the cluster details page.

#. If Kerberos authentication is enabled for the cluster, perform the following steps. If Kerberos authentication is not enabled for the cluster, skip this step.

   In the **Basic Information** area on the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users. For details, see :ref:`Synchronizing IAM Users to MRS <mrs_01_0495>`.

   .. note::

      -  In MRS 1.7.2 or earlier, the job management function is unavailable in a cluster with Kerberos authentication enabled. You need to submit a job in the background.
      -  When the policy of the user group to which the IAM user belongs changes from MRS ReadOnlyAccess to MRS CommonOperations, MRS FullAccess, or MRS Administrator, wait for 5 minutes until the new policy takes effect after the synchronization is complete because the **SSSD** (System Security Services Daemon) cache of cluster nodes needs time to be updated. Then, submit a job. Otherwise, the job may fail to be submitted.
      -  When the policy of the user group to which the IAM user belongs changes from MRS CommonOperations, MRS FullAccess, or MRS Administrator to MRS ReadOnlyAccess, wait for 5 minutes until the new policy takes effect after the synchronization is complete because the **SSSD** cache of cluster nodes needs time to be updated.

#. Click the **Jobs** tab.

#. Click **Create**. The **Create Job** page is displayed.

#. Set **Type** to **Flink**. Configure Flink job information by referring to :ref:`Table 1 <mrs_01_0527__tf38a01bf69f34c29a25317555fc32b92>`.

   .. _mrs_01_0527__tf38a01bf69f34c29a25317555fc32b92:

   .. table:: **Table 1** Job configuration information

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                               |
      +===================================+===========================================================================================================================================================================================================================================================================+
      | Name                              | Job name. It contains 1 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                           |
      |                                   | .. note::                                                                                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                           |
      |                                   |    You are advised to set different names for different jobs.                                                                                                                                                                                                             |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Program Path                      | Path of the program package to be executed. The following requirements must be met:                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                           |
      |                                   | -  Contains a maximum of 1,023 characters, excluding special characters such as\ ``;|&><'$.`` The parameter value cannot be empty or full of spaces.                                                                                                                      |
      |                                   | -  The path of the program to be executed can be stored in HDFS or OBS. The path varies depending on the file system.                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                           |
      |                                   |    -  OBS: The path must start with **obs://**. Example: **obs://wordcount/program/xxx.jar**                                                                                                                                                                              |
      |                                   |    -  HDFS: The path must start with **/user**. For details about how to import data to HDFS, see :ref:`Importing Data <en-us_topic_0019489057__section6302178417377>`.                                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Program Parameter                 | (Optional) Used to configure optimization parameters such as threads, memory, and vCPUs for the job to optimize resource usage and improve job execution performance.                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                           |
      |                                   | :ref:`Table 2 <mrs_01_0527__table15713101071912>` describes the common parameters of a running program.                                                                                                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameters                        | (Optional) Key parameter for program execution. The parameter is specified by the function of the user's program. MRS is only responsible for loading the parameter. Multiple parameters are separated by space.                                                          |
      |                                   |                                                                                                                                                                                                                                                                           |
      |                                   | The parameter contains a maximum of 150,000 characters. It cannot contain special characters\ ``;|&><'$,`` but can be left blank.                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                                           |
      |                                   | .. caution::                                                                                                                                                                                                                                                              |
      |                                   |                                                                                                                                                                                                                                                                           |
      |                                   |    CAUTION:                                                                                                                                                                                                                                                               |
      |                                   |    If you enter a parameter with sensitive information (such as the login password), the parameter may be exposed in the job details display and log printing. Exercise caution when performing this operation.                                                           |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Service Parameter                 | (Optional) It is used to modify service parameters for the job. The parameter modification applies only to the current job. To make the modification take effect permanently for the cluster, follow instructions in :ref:`Configuring Service Parameters <mrs_01_0204>`. |
      |                                   |                                                                                                                                                                                                                                                                           |
      |                                   | To add multiple parameters, click |image1| on the right. To delete a parameter, click **Delete** on the right.                                                                                                                                                            |
      |                                   |                                                                                                                                                                                                                                                                           |
      |                                   | :ref:`Table 3 <mrs_01_0527__table1583911183234>` describes the common parameters of a service.                                                                                                                                                                            |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Command Reference                 | Command submitted to the background for execution when a job is submitted.                                                                                                                                                                                                |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. _mrs_01_0527__table15713101071912:

   .. table:: **Table 2** Program parameters

      +-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------+
      | Parameter | Description                                                                                                                                                                         | Example Value        |
      +===========+=====================================================================================================================================================================================+======================+
      | -ytm      | Memory size of each TaskManager container. (Optional unit. The unit is MB by default.)                                                                                              | 1024                 |
      +-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------+
      | -yjm      | Memory size of JobManager container. (Optional unit. The unit is MB by default.)                                                                                                    | 1024                 |
      +-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------+
      | -yn       | Number of Yarn containers allocated to applications. The value is the same as the number of TaskManagers.                                                                           | 2                    |
      +-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------+
      | -ys       | Number of TaskManager cores.                                                                                                                                                        | 2                    |
      +-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------+
      | -ynm      | Custom name of an application on Yarn.                                                                                                                                              | test                 |
      +-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------+
      | -c        | Class of the program entry point (for example, the **main** or **getPlan()** method). This parameter is required only when the JAR file does not specify the class of its manifest. | com.bigdata.mrs.test |
      +-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------+

   .. note::

      For MRS 3.x or later, the **-yn** parameter is not supported.

   .. _mrs_01_0527__table1583911183234:

   .. table:: **Table 3** Service parameters

      +-------------------+----------------------------------------------------+---------------+
      | Parameter         | Description                                        | Example Value |
      +===================+====================================================+===============+
      | fs.obs.access.key | Key ID for accessing OBS.                          | ``-``         |
      +-------------------+----------------------------------------------------+---------------+
      | fs.obs.secret.key | Key corresponding to the key ID for accessing OBS. | ``-``         |
      +-------------------+----------------------------------------------------+---------------+

#. Confirm job configuration information and click **OK**.

   After the job is created, you can manage it.

Submitting a Job in the Background
----------------------------------

In MRS 3.x and later versions, the default installation path of the client is /opt/Bigdata/client. In MRS 3.x and earlier versions, the default installation path is /opt/client. For details, see the actual situation.

#. Log in to the MRS client.

#. Run the following command to initialize environment variables:

   **source /opt/Bigdata/client/bigdata_env**

#. If Kerberos authentication is enabled for the cluster, perform the following steps. If Kerberos authentication is not enabled for the cluster, skip this step.

   a. Prepare a user for submitting Flink jobs.

   b. Log in to Manager as the newly created user.

      -  For MRS 3.x earlier: Log in to Manager of the cluster. Choose **System** > **Manage User**. In the **Operation** column of the row that contains the added user, choose **More** > **Download authentication credential** to locate the row that contains the user.
      -  For MRS 3.\ *x* or later: Log in to Manager of the cluster. Choose **System** > **Permission** > **Manage User**. On the displayed page, locate the row that contains the added user, click **More** in the **Operation** column, and select **Download authentication credential**.

   c. Decompress the downloaded authentication credential package and copy the **user.keytab** file to the client node, for example, to the **/opt/Bigdata/client/Flink/flink/conf** directory on the client node. If the client is installed on a node outside the cluster, copy the **krb5.conf** file to the **/etc/** directory on this node.

   d. For MRS 3.x or later: In security mode, add the service IP address of the node where the client is installed and floating IP address of Manager to the **jobmanager.web.allow-access-address** configuration item in the **/opt/Bigdata/client/Flink/flink/conf/flink-conf.yaml** file.

   e. Run the following commands to configure security authentication by adding the **keytab** path and username to the **/opt/Bigdata/client/Flink/flink/conf/flink-conf.yaml** configuration file.

      **security.kerberos.login.keytab:** *<user.keytab file path>*

      **security.kerberos.login.principal:** *<Username>*

      Example:

      security.kerberos.login.keytab: /opt/Bigdata/client/Flink/flink/conf/user.keytab

      security.kerberos.login.principal: test

   f. Run the following command to perform security hardening in the **bin** directory of the Flink client. Set password to a new password for submitting jobs.

      sh generate_keystore.sh <*password*>

      This script automatically replaces the SSL value in the **/opt/Bigdata/client/Flink/flink/conf/flink-conf.yaml** file. For MRS 3.x or earlier, external SSL is disabled by default in security clusters. To enable external SSL, run this script again after configuration. The configuration parameters do not exist in the default Flink configuration of MRS, if you enable SSL for external connections, you need to add the parameters listed in :ref:`Table 4 <mrs_01_0527__table780265116214>`.

      .. _mrs_01_0527__table780265116214:

      .. table:: **Table 4** Parameter description

         +---------------------------------------+--------------------------+-------------------------------------------------------------------------------------------+
         | Parameter                             | Example Value            | Description                                                                               |
         +=======================================+==========================+===========================================================================================+
         | security.ssl.rest.enabled             | true                     | Switch to enable external SSL.                                                            |
         +---------------------------------------+--------------------------+-------------------------------------------------------------------------------------------+
         | security.ssl.rest.keystore            | ${path}/flink.keystore   | Path for storing **keystore**.                                                            |
         +---------------------------------------+--------------------------+-------------------------------------------------------------------------------------------+
         | security.ssl.rest.keystore-password   | 123456                   | Password of the **keystore**. **123456** indicates a user-defined password is required.   |
         +---------------------------------------+--------------------------+-------------------------------------------------------------------------------------------+
         | security.ssl.rest.key-password        | 123456                   | Password of the SSL key. **123456** indicates a user-defined password is required.        |
         +---------------------------------------+--------------------------+-------------------------------------------------------------------------------------------+
         | security.ssl.rest.truststore          | ${path}/flink.truststore | Path for storing the **truststore**.                                                      |
         +---------------------------------------+--------------------------+-------------------------------------------------------------------------------------------+
         | security.ssl.rest.truststore-password | 123456                   | Password of the **truststore**. **123456** indicates a user-defined password is required. |
         +---------------------------------------+--------------------------+-------------------------------------------------------------------------------------------+

      .. note::

         -  For MRS 3.x or earlier: The **generate_keystore.sh** script is automatically generated.

         -  Perform `authentication and encryption <https://docs.otc.t-systems.com/cmpntguide/mrs/mrs_01_1583.html>`__. The generated **flink.keystore**, **flink.truststore**, and **security.cookie** files are automatically filled in the corresponding configuration items in **flink-conf.yaml**.

         -  For MRS 3.\ *x* or later: You can obtain the values of **security.ssl.key-password**, **security.ssl.keystore-password**, and **security.ssl.truststore-password** using the Manager plaintext encryption API by running the following command:

            **curl -k -i -u <user name>:<password> -X POST -HContent-type:application/json -d '{"plainText":"<password>"}' 'https://x.x.x.x:28443/web/api/v2/tools/encrypt'**; In the preceding command, <*password*> must be the same as the password used for issuing the certificate, and *x.x.x.x* indicates the floating IP address of Manager in the cluster.

   g. Configure paths for the client to access the **flink.keystore** and **flink.truststore** files.

      -  Absolute path: After the script is executed, the file path of **flink.keystore** and **flink.truststore** is automatically set to the absolute path **opt/Bigdata/client/Flink/flink/conf/** in the **flink-conf.yaml** file. In this case, you need to move the **flink.keystore** and **flink.truststore** files from the **conf** directory to this absolute path on the Flink client and Yarn nodes.
      -  Relative path: Perform the following steps to set the file path of **flink.keystore** and **flink.truststore** to the relative path and ensure that the directory where the Flink client command is executed can directly access the relative paths.

         #. In the **/opt/Bigdata/client/Flink/flink/conf/**\ directory, create a new directory, for example, **ssl**.

         #. Move the **flink.keystore** and **flink.truststore** file to the /**opt/Bigdata/client/Flink/flink/conf/ssl/** directory.

         #. For MRS 3.\ *x* or later: Change the values of the following parameters in the **flink-conf.yaml** file to relative paths:

            .. code-block::

               security.ssl.keystore: ssl/flink.keystore
               security.ssl.truststore: ssl/flink.truststore

         #. For MRS 3.x or earlier: Change the values of the following parameters in the **flink-conf.yaml** file to relative paths:

            .. code-block::

               security.ssl.internal.keystore: ssl/flink.keystore
               security.ssl.internal.truststore: ssl/flink.truststore

   h. If the client is installed on a node outside the cluster, add the following configuration to the configuration file (for example, **/opt/Bigdata/client/Flink/fink/conf/flink-conf.yaml**). Replace **xx.xx.xxx.xxx** with the IP address of the node where the client resides.

      .. code-block::

         web.access-control-allow-origin: xx.xx.xxx.xxx
         jobmanager.web.allow-access-address: xx.xx.xxx.xxx

#. Run a wordcount job.

   -  Normal cluster (Kerberos authentication disabled)

      -  Run the following commands to start a session and submit a job in the session:

         .. code-block::

            yarn-session.sh -nm "session-name"
            flink run /opt/Bigdata/client/Flink/flink/examples/streaming/WordCount.jar

      -  Run the following command to submit a single job on Yarn:

         .. code-block::

            flink run -m yarn-cluster /opt/Bigdata/client/Flink/flink/examples/streaming/WordCount.jar

   -  Security cluster (Kerberos authentication enabled)

      -  If the **flink.keystore** and **flink.truststore** file are stored in the absolute path:

         -  Run the following commands to start a session and submit a job in the session:

            .. code-block::

               yarn-session.sh -nm "session-name"
               flink run /opt/Bigdata/client/Flink/flink/examples/streaming/WordCount.jar

         -  Run the following command to submit a single job on Yarn:

            .. code-block::

               flink run -m yarn-cluster /opt/Bigdata/client/Flink/flink/examples/streaming/WordCount.jar

      -  If the **flink.keystore** and **flink.truststore** file are stored in the relative path:

         -  In the same directory of SSL, run the following command to start a session and submit jobs in the session. The SSL directory is a relative path. For example, if the SSL directory is **opt/Bigdata/client/Flink/flink/conf/**, then run the following command in this directory:

            .. code-block::

               yarn-session.sh -t ssl/ -nm "session-name"
               flink run /opt/Bigdata/client/Flink/flink/examples/streaming/WordCount.jar

         -  Run the following command to submit a single job on Yarn:

            .. code-block::

               flink run -m yarn-cluster -yt ssl/ /opt/Bigdata/client/Flink/flink/examples/streaming/WordCount.jar

.. |image1| image:: /_static/images/en-us_image_0000001349137577.png
