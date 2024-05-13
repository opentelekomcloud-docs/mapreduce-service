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

**Modify client information.**

5. Modify information about the manually registered client.

   On the **Client Management** page, select the target client and click **Modify**. After modifying the information, click **OK**.

**Delete client information.**

6. On the **Client Management** page, select the target client and click **Delete**. In the displayed dialog box, click **OK**.

   To delete multiple clients, select the all of them and click **Batch Delete**. In the displayed dialog box, click **OK**.

**Export client information.**

7. On the **Client Management** page, click **Export All** to export information about all registered clients to the local PC.

   .. note::

      On the **Client Management** page, only components that have clients are displayed in the component list. Therefore, some components that do not have clients and have special components are not displayed.

      The following components are not displayed:

      LdapServer, KrbServer, DBService, Hue, MapReduce, and Flume
