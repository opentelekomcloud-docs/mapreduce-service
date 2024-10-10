:original_name: mrs_01_248978.html

.. _mrs_01_248978:

Interconnecting the Guardian Service with OBS
=============================================

Scenario
--------

This section describes how to enable storage and compute decoupling for the Guardian component. After this feature is enabled, Guardian can provide temporary authentication credentials for services such as HDFS, Hive, Spark, Loader, and HetuEngine to access OBS when decoupled storage and compute are used.

Perform the following steps to interconnect Guardian with OBS:

#. :ref:`Creating an OBS Parallel File System <mrs_01_248978__en-us_topic_0000001705424181_section84751202314>`
#. :ref:`Creating a Cloud Service Agency and Binding It to a Cluster <mrs_01_248978__en-us_topic_0000001705424181_section18450819223>`
#. :ref:`Creating an Agency for a Regular Account <mrs_01_248978__en-us_topic_0000001705424181_section189891846103018>`
#. :ref:`Configuring a Cloud Service Agency <mrs_01_248978__en-us_topic_0000001705424181_section543793710440>`
#. :ref:`Granting OBS Access Permission to Guardian <mrs_01_248978__en-us_topic_0000001705424181_section14856212218>`
#. :ref:`Enabling Cascading Authorization for Hive Tables <mrs_01_248978__en-us_topic_0000001705424181_section1298115261245>`
#. :ref:`Configuring the Recycle Bin Cleanup Policy <mrs_01_248978__en-us_topic_0000001705424181_section335573320413>`

Prerequisites
-------------

-  Components such as Guardian, Ranger, and Hadoop have been installed in the cluster.
-  If Guardian is installed after components such as Hadoop, HetuEngine, Hive, and Spark are installed, the Guardian client must be downloaded again and the default client for job submission on the management plane must be refreshed.

Impact on the System
--------------------

-  After the configuration is complete, you need to refresh the configuration of the original client or reinstall the client.
-  To submit a job on console, log in to the active OMS node as user **omm** and run the **sh /opt/executor/bin/refresh-client-config.sh** command to refresh the built-in client of the cluster.

.. _mrs_01_248978__en-us_topic_0000001705424181_section84751202314:

Creating an OBS Parallel File System
------------------------------------

#. Log in to the OBS console.

#. Choose **Parallel File Systems** > **Create Parallel File System**.

#. Enter a file system name, for example, **guardian-obs**.

   The name of an enterprise project must be the same as that of the MRS cluster. Set other parameters.

#. Click **Create Now**.

.. _mrs_01_248978__en-us_topic_0000001705424181_section18450819223:

Creating a Cloud Service Agency and Binding It to a Cluster
-----------------------------------------------------------

#. Log in to the management console.
#. In the service list, choose **Management & Governance** > **Identity and Access Management**.
#. Choose **Agencies**. On the displayed page, click **Create Agency**.
#. Set the agency name, for example, **mrs_ecs_obs**.
#. Set **Agency Type** to **Cloud service** and select **Elastic Cloud Server (ECS) and Bare Metal Server (BMS)** to authorize ECS or BMS to invoke OBS.
#. Set **Validity Period** to **Unlimited** and click **Next**.
#. On the displayed page, search for the **OBS OperateAccess** policy and enable it.
#. Click **Next**, select **All resources**, click **Show More**, select **Global resources**, and click **OK**.
#. In the dialog box that is displayed, click **OK** to start authorization. After "**Authorization successful.**" is displayed, click **Finish**. The agency is successfully created.
#. Log in to the MRS console. In the navigation pane on the left, choose **Active Clusters**.
#. Click the name of the target cluster to go to details page.
#. In the **Dashboard** tab, click **Synchronize** on the right of **IAM User Sync** to synchronize the IAM user.
#. In the **Dashboard** tab, click **Manage Agency** on the right of **Agency**, select the created agency, for example, **mrs_ecs_obs**, and click **OK** to bind the agency to the cluster.

.. _mrs_01_248978__en-us_topic_0000001705424181_section189891846103018:

Creating an Agency for a Regular Account
----------------------------------------

#. Log in to the management console.

#. In the service list, choose **Management & Governance** > **Identity and Access Management**.

#. Choose **Agencies**. On the displayed page, click **Create Agency**.

#. Enter an agency name, for example, **agency-MRS-to-OBS**.

#. Set **Agency Type** to **Account**.

#. Enter your cloud account for **Delegated Account**, that is, the account you register using your mobile phone number. It cannot be a federated user or an IAM user created using your cloud account.

#. Set **Validity Period** to **Unlimited** and click **Next**.

#. On the displayed page, search for the **OBS Administrator** policy and enable it.

#. Click **Next**, select **All resources**, click **Show More**, select **Global resources**, and click **OK**.

#. .. _mrs_01_248978__en-us_topic_0000001705424181_li28688513432:

   After the agency is created, check and record the agency ID.

.. _mrs_01_248978__en-us_topic_0000001705424181_section543793710440:

Configuring a Cloud Service Agency
----------------------------------

#. Log in to the management console.

#. In the service list, choose **Management & Governance** > **Identity and Access Management**.

#. Select **Agencies** and click the agency **mrs_ecs_obs** created in :ref:`Creating a Cloud Service Agency and Binding It to a Cluster <mrs_01_248978__en-us_topic_0000001705424181_section18450819223>`

#. .. _mrs_01_248978__en-us_topic_0000001705424181_li92351945184612:

   Choose **Permissions** > **Authorize**, click **Create Policy** in the upper right corner, and set the parameters as follows:

   -  **Policy Name**: Enter a policy name, for example, **guardian-assume-policy**.

   -  **Policy View**: Select **JSON**.

   -  **Policy Content**: Configure the policy as follows. *{Agency ID}* indicates the ID recorded in :ref:`10 <mrs_01_248978__en-us_topic_0000001705424181_li28688513432>`.

      .. code-block::

         {
             "Version": "1.1",
             "Statement": [
                 {
                     "Action": [
                         "iam:agencies:assume"
                     ],
                     "Resource": {
                         "uri": [
                             "/iam/agencies/{Agency ID}"
                         ]
                     },
                     "Effect": "Allow"
                 }
             ]
         }

#. Click **Next**. On the **Select Policy/Role** page, select the policy created in :ref:`4 <mrs_01_248978__en-us_topic_0000001705424181_li92351945184612>`.

#. Click **Next**, select **All resources**, click **Show More**, select **Global resources**, and click **OK**.

.. _mrs_01_248978__en-us_topic_0000001705424181_section14856212218:

Granting OBS Access Permission to Guardian
------------------------------------------

#. Log in to FusionInsight Manager, choose **Cluster** > **Services** > **Guardian**, click **Configurations**, and then **All Configurations**. On the displayed page, search for and modify the following parameters.

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | Parameter                             | Description                                                                                                                                                                                    | Value                                                                                   |
   +=======================================+================================================================================================================================================================================================+=========================================================================================+
   | fs.obs.guardian.accesslabel.enabled   | Whether to enable **access label** for using Guardian to connect to OBS.                                                                                                                       | true                                                                                    |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | fs.obs.guardian.enabled               | Whether to enable Guardian.                                                                                                                                                                    | true                                                                                    |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | fs.obs.delegation.token.providers     | Delegation token generator. If **fs.obs.guardian.enabled** is set to **true**, configure both **com.example.mrs.dt.MRSDelegationTokenProvider** and **com.example.mrs.dt.GuardianDTProvider**. | com.example.mrs.dt.MRSDelegationTokenProvider and com.example.mrs.dt.GuardianDTProvider |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | token.server.access.label.agency.name | Name of the specified IAM agency, which is the agency created in :ref:`Creating an Agency for a Regular Account <mrs_01_248978__en-us_topic_0000001705424181_section189891846103018>`.         | agency-MRS-to-OBS                                                                       |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------+

#. Save the service configuration, choose **More** > **Restart Configuration-Expired Instances** on the FusionInsight Manager home page, and restart all service instances whose configurations have expired as prompted.

#. To submit jobs on the MRS console, log in to the active OMS node as user **omm** and run the following command to refresh the built-in client configuration:

   **sh /opt/executor/bin/refresh-client-config.sh**

.. _mrs_01_248978__en-us_topic_0000001705424181_section1298115261245:

Enabling Cascading Authorization for Hive Tables
------------------------------------------------

#. Log in to FusionInsight Manager, choose **Cluster** > **Services** > **Ranger** and click **Configurations**.

#. Search for the **ranger.ext.authorization.cascade.enable** parameter and set it to **true**.

   |image1|

#. Click **Save**.

#. Click **Instance** and select all RangerAdmin instances. Click **More** and select **Restart Instance**. Enter the password, and click **OK** to restart all RangerAdmin instances.

.. _mrs_01_248978__en-us_topic_0000001705424181_section335573320413:

Configuring the Recycle Bin Cleanup Policy
------------------------------------------

#. Log in to the OBS Console.

#. Select **Parallel File Systems** and click the file system created in :ref:`Creating an OBS Parallel File System <mrs_01_248978__en-us_topic_0000001705424181_section84751202314>`.

#. Choose **Basic Configurations** > **Lifecycle Rules** and click **Create** to create a lifecycle rule for the **/user/.Trash** directory.

   .. caution::

      **For clusters that use decoupled storage and compute, configure a lifecycle policy for the related directories by referring to this chapter. Otherwise, the storage space may be used up and storage fees may increase.**

   .. table:: **Table 1** Parameters for creating a lifecycle rule

      +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+
      | Parameter                                    | Description                                                                                                                                                                                                                                                                                                                                                        | Example     |
      +==============================================+====================================================================================================================================================================================================================================================================================================================================================================+=============+
      | Status                                       | Whether to enable the lifecycle rule.                                                                                                                                                                                                                                                                                                                              | Enable      |
      +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+
      | Rule Name                                    | User-defined rule name, which is used to identify different lifecycle configurations.                                                                                                                                                                                                                                                                              | rule-test   |
      +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+
      | Prefix                                       | Prefix of the objects to which the lifecycle rule applies. Generally, the recycle bin directory of MRS components is **/user/.Trash**.                                                                                                                                                                                                                             | user/.Trash |
      +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+
      | Transition to Infrequent Access After (Days) | Number of days before transitioning to infrequent access after the object is last updated. The value of this parameter must be at least **30**.                                                                                                                                                                                                                    | 30 days     |
      +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+
      | Transition to Archive After (Days)           | Number of days before transitioning to archive after the object is last updated. If **Transition to Infrequent Access After (Days)** is also configured, after the lifecycle is transitioned to infrequent access, wait at least 30 days before transitioning it to archive. If only **Transition to Archive After (Days)** is configured, there is no time limit. | 31 days     |
      +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+
      | Delete Files After (Days)                    | Number of days before being deleted by OBS after the object is last updated. This parameter must be larger than the above two parameters.                                                                                                                                                                                                                          | 32 days     |
      +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+
      | Delete Fragments After (Days)                | Number of days before fragments are expired and deleted by OBS automatically.                                                                                                                                                                                                                                                                                      | 30 days     |
      +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+

#. Click **OK** to complete the lifecycle rule configuration.

   To modify the lifecycle configuration, locate the lifecycle rule, click **Edit** or **Disable** on the right. Click **Enable** to enable the lifecycle rule.

.. |image1| image:: /_static/images/en-us_image_0000002009573745.png
