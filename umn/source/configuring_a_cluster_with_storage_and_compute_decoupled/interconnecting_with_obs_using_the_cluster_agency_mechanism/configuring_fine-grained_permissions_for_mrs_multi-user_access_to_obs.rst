:original_name: mrs_01_0632.html

.. _mrs_01_0632:

Configuring Fine-Grained Permissions for MRS Multi-User Access to OBS
=====================================================================

When fine-grained permission control is enabled, you can configure OBS access permissions to implement access control on directories in OBS file systems.

.. note::

   This section applies only to MRS 2.\ *x* or earlier (excluding MRS 1.9.2).

This function enables you to control MRS users' access to OBS resources. For example, if you allow user group A to only access log files in a specified OBS file system, perform the following operations:

#. Configure an agency with OBS access permissions for an MRS cluster so that OBS can be accessed using the temporary AK/SK automatically obtained by the ECS. This prevents the AK/SK from being exposed in the configuration file.
#. Create a policy on the IAM console to allow access to log files in a specified OBS file system, and create an agency bound to the policy permission.
#. In the MRS cluster, bind the new agency to user group A so that user group A only has the permission to access log files in the specified OBS file system.

In the following scenarios, the username used for submitting jobs is an internal username so that MRS multi-user access to OBS is not supported.

-  For spark-beeline, the internal username used for submitting jobs is **spark** in a security cluster and **omm** in a normal cluster.
-  For the HBase shell, the internal username used for submitting jobs is **hbase** in a security cluster and **omm** in a normal cluster.
-  For Presto, the internal username used for submitting jobs in the security cluster is **omm** or **hive**, and that in the normal cluster is **omm**. (Choose **Components** > **Presto** > **Service Configuration**. Change **Basic** to **All** in the parameter type drop-down box.) Then, search for and change the value of **hive.hdfs.impersonation.enabled** to **true** to enable MRS multi-user to access OBS with fine-grained permissions.

Prerequisites
-------------

-  Fine-grained permission control has been enabled. For details about permissions management, see :ref:`Creating an MRS User <mrs_01_0453>`.
-  You have a basic knowledge of **IAM Agencies** (see section "Agencies" in the *IAM User Guide*) and OBS fine-grained policies.

Step 1: Configuring an Agency with OBS Access Permission for a Cluster
----------------------------------------------------------------------

Follow instructions in :ref:`Configuring a Storage-Compute Decoupled Cluster (Agency) <mrs_01_0768>` to configure an agency with OBS access permissions.

The agency takes effect for all users (including internal users) and user groups in the cluster. To control the permissions of users and user groups in the cluster to access OBS, perform the following operations.

.. note::

   When you configure permissions on an OBS path, if the write permission is configured, you need to configure the corresponding recycle bin path.

   The default recycle bin path is **/user/${current.user}/.Trash/**, in which **${current.user}** indicates the current user.

Step 2: Creating a Policy and an Agency on IAM
----------------------------------------------

Create policies with different access permissions and bind the policies to the agency. For details, see :ref:`Creating a Policy and an Agency on IAM <mrs_01_0632__section163381225399>`.

Step 3: Configuring OBS Permission Control Mappings on the MRS Cluster Details Page
-----------------------------------------------------------------------------------

#. On the MRS management console, choose **Clusters** > **Active Clusters** and click the cluster name.

#. In the **Basic Information** area on the **Dashboard** tab page, click **Manage** next to **OBS Permission Control**.

#. Click **Add Mapping** and set parameters according to :ref:`Table 1 <mrs_01_0632__table175454305220>`.

   .. _mrs_01_0632__table175454305220:

   .. table:: **Table 1** OBS permission control parameters

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                        |
      +===================================+====================================================================================================================================================================================================================================================================+
      | IAM Agency                        | Select the agency created in :ref:`2 <mrs_01_0632__li1894924154514>`.                                                                                                                                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Type                              | -  **User**: User-level mapping                                                                                                                                                                                                                                    |
      |                                   | -  **Group**: User group-level mapping                                                                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                    |
      |                                   | .. note::                                                                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                    |
      |                                   |    -  User-level mapping takes priority over user group-level mapping. If you select **Group**, you are advised to enter the primary group name in **MRS User (User Group)**.                                                                                      |
      |                                   |    -  Do not use the same username (user group) for multiple mapping records.                                                                                                                                                                                      |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | MRS User (User Group)             | Use commas (,) to separate multiple names of users or user groups.                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                    |
      |                                   | .. note::                                                                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                    |
      |                                   |    -  If OBS permission control is not configured for a user and no AK and SK are configured, the OBS Operator permission in **MRS_ECS_DEFAULT_AGENCY** will be used for accessing OBS. You are advised not to bind the internal user of a component to an agency. |
      |                                   |    -  If you need to configure an agency for the internal user of a component when submitting a job in the following scenarios, the requirements are as follows:                                                                                                   |
      |                                   |                                                                                                                                                                                                                                                                    |
      |                                   |       -  To control permissions on spark-beeline operations, set the username to **spark** for a security cluster and **omm** for a normal cluster.                                                                                                                |
      |                                   |       -  To control permissions on HBase shell operations, set the username to **hbase** for a security cluster and **omm** for a normal cluster.                                                                                                                  |
      |                                   |       -  To control permissions on Presto, set the username to **omm**, **hive**, and the username used for logging in to the client for a security cluster and **omm** and the username used for logging in to the client for a normal cluster.                   |
      |                                   |       -  If you want to use Hive to create tables in beeline mode, set the username to the internal user **hive**.                                                                                                                                                 |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

#. Select **I agree to authorize the trust relationships between MRS Users (Groups) and IAM agencies**, and click **OK**. The mapping between the MRS user and OBS permission is added.

   If |image1| appears next to **OBS Permission Control** on the **Dashboard** tab page or the mapping table has been updated for OBS permission control, the mapping takes effect. It takes about 1 minute to for the mapping to take effect.

   In the **Operation** column of the mapping list, you can edit or delete the added mapping.

   .. note::

      -  If OBS permission control is not configured for a user and no AK and SK are configured, the permissions owned by the agency configured for the cluster in the **Object Storage Service (OBS)** project will be used to access OBS.
      -  Regardless of whether OBS permission control is configured, AK/SK permission is used for accessing OBS once it is configured.
      -  Security Administrator permission is required to modify, create, or delete a mapping.
      -  To enable mapping changes to take effect in spark-line, hive beeline and Presto respectively, you need to restart Spark, exit beeline and enter again, and restart Presto respectively.

Component Access to OBS When OBS Permission Control Is Enabled
--------------------------------------------------------------

#. Log in to any node in a cluster as user **root** using the password set during cluster creation.

#. Set environment variables (In MRS 3.x and later versions, the default installation path of the client is /opt/Bigdata/client. In MRS 3.x and earlier versions, the default installation path is /opt/client. For details, see the actual situation.).

   **source /opt/Bigdata/client/bigdata_env**

#. If the Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user. If the Kerberos authentication is disabled for the current cluster, skip this step:

   **kinit** **MRS cluster user**

   Example: **kinit admin**

#. If the Kerberos authentication is disabled for the current cluster, run the following commands to log in. Note that you should create a user that belongs to the **supergroup** group by referring to :ref:`Creating a User <mrs_01_0345>` and replace *XXXX* with the username:

   **mkdir /home/XXXX**

   **chown XXXX /home/XXXX**

   **su - XXXX**

#. Access OBS. You do not need to configure the AK, SK, and endpoint. The OBS path format is **obs://buck_name/**\ **XXX**.

   Example: **hadoop fs -ls "obs://obs-example/job/hadoop-mapreduce-examples-3.1.2.jar"**

   .. note::

      -  If you want to use **hadoop fs** to delete files on OBS, use **hadoop fs -rm -skipTrash** to delete the files.
      -  If data import is not involved when a table is created using spark-sql and spark-beeline, OBS will not be accessed. That is, if you create a table in an OBS directory on which you do not have permission, the **CREATE TABLE** operation will still be successful, but the error message "**403 AccessDeniedException**" is displayed when you insert data.

.. _mrs_01_0632__section163381225399:

Creating a Policy and an Agency on IAM
--------------------------------------

#. .. _mrs_01_0632__li20781191935317:

   Create a policy on IAM.

   a. Log in to the IAM console.

   b. Choose **Permissions**. On the displayed page, click **Create Custom Policy**.

   c. Set parameters according to :ref:`Table 2 <mrs_01_0632__table4781201918533>`. Obtain the customized OBS policy samples that are frequently used by referring to .

      .. _mrs_01_0632__table4781201918533:

      .. table:: **Table 2** Policy parameters

         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                             |
         +===================================+=========================================================================================================================================================================================================================================================================================================================================================================+
         | Policy Name                       | Only letters, digits, spaces, and special characters (-_.,) are allowed.                                                                                                                                                                                                                                                                                                |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Scope                             | Select **Global services**, because OBS is a global service.                                                                                                                                                                                                                                                                                                            |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Policy View                       | Select **Visual editor**.                                                                                                                                                                                                                                                                                                                                               |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Policy Content                    | #. **Allow**: Select **Allow**.                                                                                                                                                                                                                                                                                                                                         |
         |                                   | #. **Select service**: Select **Object Storage Service (OBS)**.                                                                                                                                                                                                                                                                                                         |
         |                                   | #. **Select action**: Select **WriteOnly**, **ReadOnly**, and **ListOnly**.                                                                                                                                                                                                                                                                                             |
         |                                   | #. **Specific resources**:                                                                                                                                                                                                                                                                                                                                              |
         |                                   |                                                                                                                                                                                                                                                                                                                                                                         |
         |                                   |    #. Set **object** to **Specify resource path**, click **Add Resource Path**, and enter *obs_bucket_name/*\ **tmp/** and *obs_bucket_name*\ **/tmp/\***. The **/tmp** directory is used as an example. If you need to add permissions for other directories, perform the following steps to add the directories and resource paths of all objects in the directories. |
         |                                   |    #. Set **bucket** to **Specify resource path**, click **Add Resource Path**, and enter *obs_bucket_name*.                                                                                                                                                                                                                                                            |
         |                                   |                                                                                                                                                                                                                                                                                                                                                                         |
         |                                   | #. (Optional) Add request condition, which does not need to be added currently.                                                                                                                                                                                                                                                                                         |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Description                       | (Optional) Brief description about the policy.                                                                                                                                                                                                                                                                                                                          |
         +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

      .. note::

         If the data write operation of each component is implemented in **rename** mode, the permission to delete objects must be configured when data is written.

   d. Click **OK** to save the policy.

#. .. _mrs_01_0632__li1894924154514:

   Create an agency on IAM.

   a. Log in to the IAM console.

   b. Choose **Agencies**. On the displayed page, click **Create Agency**.

   c. Set parameters according to :ref:`Table 3 <mrs_01_0632__table4901145420452>`.

      .. _mrs_01_0632__table4901145420452:

      .. table:: **Table 3** Agency parameters

         +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                                                                                |
         +===================================+============================================================================================================================================================================+
         | Agency Name                       | Only letters, digits, spaces, and special characters (-_.,) are allowed.                                                                                                   |
         +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Agency Type                       | Select **Common account**.                                                                                                                                                 |
         +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Delegated Account                 | Enter your cloud account, that is, the account you register using your mobile phone number. It cannot be a federated user or an IAM user created using your cloud account. |
         +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Validity Period                   | Set this parameter as required.                                                                                                                                            |
         +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Description                       | (Optional) Brief description about the agency.                                                                                                                             |
         +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
         | Permissions                       | #. In the **Project [Region]** column, locate the row where **OBS** is, click **Attach Policy**.                                                                           |
         |                                   | #. Select the policy created in :ref:`1 <mrs_01_0632__li20781191935317>` to display it in **Selected Policies**.                                                           |
         |                                   | #. Click **OK**.                                                                                                                                                           |
         +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   d. Click **OK** to save the agency.

      .. note::

         If you modify an agency and policies bound to it after using the agency to access OBS, the modification will take effect within 15 minutes.

.. |image1| image:: /_static/images/en-us_image_0000001349057773.png
