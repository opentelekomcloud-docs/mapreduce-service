:original_name: admin_guide_000023.html

.. _admin_guide_000023:

Batch Upgrading Clients
=======================

Scenario
--------

The client package downloaded from MRS Manager contains the client batch upgrade tool. When multiple clients need to be upgraded after the cluster upgrade or scale-out, you can use this tool to upgrade the clients in batches with a few clicks. In addition, the tool provides the lightweight function of batch updating the **/etc/hosts** file on the nodes where the clients are located.

Procedure
---------

**Prepare for the client upgrade.**

#. Log in to MRS Manager.

#. Choose **Cluster**, click the name of the desired cluster, click **More**, and select **Download Client** to download the complete client to the specified directory on the server.

   For details, see :ref:`Downloading the Client <admin_guide_000014>`.

   Decompress the downloaded client package and find the **batch_upgrade** directory, for example, **/tmp/FusionInsight-Client/FusionInsight_Cluster_1_Services_ClientConfig/batch_upgrade**.

#. Choose **Cluster**, click the name of the desired cluster, and choose **Client Management**. On the **Client Management** page, click **Export All** to export all client information to the local PC.

#. Decompress the exported client information and upload the **client-info.cfg** file to the **batch_upgrade** directory.

#. Supplement the password in the **client-info.cfg** file by referring to :ref:`Reference Information <admin_guide_000023__section596192114916>`.

**Upgrade clients in batches.**

6. Run the **sh client_batch_upgrade.sh -u -f /tmp/FusionInsight-Client/FusionInsight_Cluster_1_Services_Client.tar** **-g** **/tmp/FusionInsight-Client/FusionInsight_Cluster_1_Services_ClientConfig/batch_upgrade/client-info.cfg** command to perform the upgrade.

   .. important::

      You are advised to delete the **client-info.cfg** file as soon as possible after the upgrade because the password has been configured.

7. After the upgrade is complete, verify the upgrade result by running the **sh client_batch_upgrade.sh -c** command.
8. If the client is faulty, run the **sh client_batch_upgrade.sh -s** command to roll back the client.

   .. note::

      -  The client batch upgrade tool moves the original client to the backup directory, and then uses the client package specified by the **-f** parameter to install the client. Therefore, if the original client contains customized content, manually save the customized content from the backup directory or move the customized content to the client directory after the upgrade before running the **-c** command. The backup path on the client is *{Original client path}*\ **-backup**.
      -  The **-u** command is the prerequisite for the **-c** and **-s** commands. You can run the **-c** command to commit the upgrade or the **-s** command to perform a rollback only after the **-u** command is executed to perform an upgrade.
      -  You can run the **-u** command multiple times to upgrade only the clients that fail to be upgraded.
      -  The client batch upgrade tool also supports the clients of earlier versions.
      -  When upgrading a client installed by a non-root user, ensure that the user has the read and write permissions on the directory where the client is located and the parent directory on the target node. Otherwise, the upgrade will fail.
      -  The client package specified by the **-f** parameter must be a full client package. The client packages of a single component or some components cannot be used as the input.

.. _admin_guide_000023__section596192114916:

Reference Information
---------------------

Before upgrading clients in batches, you need to manually configure the user password for remotely logging in to the client node.

Run the **vi client-info.cfg** command to add a user password.

Example:

.. code-block::

   clientIp,clientPath,user,password
   10.10.10.100,/home/omm/client /home/omm/client2,omm,Password

The fields in the configuration file are as follows:

-  **clientIp**: indicates the IP address of the node where the client is located.
-  **clientPath**: indicates the client installation path. Multiple paths are separated by spaces. Note that the path cannot end with a slash (/).
-  **user**: indicates the username of the node.
-  **password**: indicates the user password of the node.

   .. note::

      If the execution fails, view the **node.log** file in the **work_space/log**\ \_\ *XXX* directory.
