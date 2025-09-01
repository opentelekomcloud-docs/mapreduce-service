:original_name: admin_guide_000022.html

.. _admin_guide_000022:

Managing a Client
=================

Scenario
--------

MRS Manager supports unified management of cluster client installation information. After a user downloads and installs a client, MRS Manager automatically records information about the installed (registered) client to facilitate query and management. In addition, you can manually add or modify the information about clients that are not automatically registered, for example, clients installed in earlier versions.

Procedure
---------

**View client information.**

#. Log in to MRS Manager.

#. Choose **Cluster**, click the name of the desired cluster, and choose **Client Management** to view information about clients installed in the cluster.

   You can view the IP address, installation path, component list, registration time, and installation user of the node where the client is located.

   When the client is downloaded and installed in the cluster of the latest version, the client information is automatically registered.

**Add client information.**

3. To manually add information about an installed client, click **Add** and manually add the IP address, installation path, user, platform information, and registration information of the client as prompted.
4. Configure the client information and click **OK**.

**Install MRS patches in batches.** (supported only by MRS 3.3.0 and later versions)

5. If a patch has been installed in the current cluster, select the clients on which the patch is to be installed on the **Client Management** page and choose **More** > **Batch install patches**. In the displayed dialog box, select "I accept the risk of possible service interruption during patch installation." Click **OK** to install the MRS patches on the selected client.

   .. note::

      During patch installation, clients cannot run properly and services on the clients may be interrupted.

**Modify client information.**

6. Modify information about the manually registered client.

   On the **Client Management** page, select the target client and click **Modify**. After modifying the information, click **OK**.

**Update client information** (available for MRS 3.5.0 and later versions).

7. If you modify service configuration parameters on Manager and restart the service, update the configuration of the installed client.

   -  Updating a client: On the **Client Management** page, select the client you want to update and click **Update** in the **Operation** column. Select the checkbox for risk confirmation, configure the information in :ref:`Table 1 <admin_guide_000022__table1560114251233>`, and click **OK**.
   -  Updating clients in batches: On the **Client Management** page, select the clients you want to update (the clients you selected must be installd by the same user), and choose **More** > **Batch Update**. Select the checkbox for risk confirmation, configure the information in :ref:`Table 1 <admin_guide_000022__table1560114251233>`, and click **OK**.

   .. note::

      During configuration update, clients cannot run properly and services on the clients may be interrupted.

   .. _admin_guide_000022__table1560114251233:

   .. table:: **Table 1** Parameters for updating the client configuration

      +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------+
      | Parameter                 | Description                                                                                                                                            | Example Value              |
      +===========================+========================================================================================================================================================+============================+
      | Authentication Method     | You can choose one of the following methods:                                                                                                           | Password                   |
      |                           |                                                                                                                                                        |                            |
      |                           | -  **Password**: Use the password for login.                                                                                                           |                            |
      |                           | -  **SSH private keys**: Use SSH private keys for login.                                                                                               |                            |
      |                           | -  **None**: To use this method, passwordless login needs to be enabled.                                                                               |                            |
      +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------+
      | Password/SSH Private Keys | -  This parameter is mandatory when **Authentication Method** is set to **Password**.                                                                  | xxx                        |
      |                           | -  This parameter is mandatory when **Authentication Method** is set to **SSH private keys**. Click **Select File** and select a local file to upload. |                            |
      +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------+
      | Host Port                 | Host port of the node where the client is to be updated                                                                                                | 22                         |
      +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------+
      | Installation Package Path | Path for storing the installation package of the updated client                                                                                        | /tmp/FusionInsight-Client/ |
      |                           |                                                                                                                                                        |                            |
      |                           | If there is already a client file in the path, it will be overwritten. For a remote node, write permission for the path is required.                   |                            |
      +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------+

**Delete client information.**

8. On the **Client Management** page, select the target client and click **Delete**. In the displayed dialog box, click **OK**.

   To delete multiple clients, select the all of them and click **Batch Delete**. In the displayed dialog box, click **OK**.

**Export client information.**

9. On the **Client Management** page, click **Export All** to export information about all registered clients to the local PC.

   .. note::

      On the **Client Management** page, only components that have clients are displayed in the component list. Therefore, some components that do not have clients and have special components are not displayed.

      The following components are not displayed:

      LdapServer, KrbServer, DBService, Hue, MapReduce, and Flume
