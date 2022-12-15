:original_name: mrs_01_0354.html

.. _mrs_01_0354:

Configuring Cross-Cluster Mutual Trust Relationships
====================================================

Scenario
--------

If cluster A needs to access the resources of cluster B, the mutual trust relationship must be configured between these two clusters.

If no trust relationship is configured, resources of a cluster are available only for users in this cluster. MRS automatically assigns a unique **domain name** for each cluster to define the scope of resources for users.

.. note::

   The operations described in this section apply only to clusters of versions earlier than MRS 3.x.

   For clusters of **MRS 3.\ x** or later, see :ref:`Configuring Cross-Manager Mutual Trust Between Clusters <admin_guide_000177>`.

Impact on the System
--------------------

-  After cross-cluster mutual trust is configured, resources of a cluster become available for users in other cluster. User permission in the clusters must be regularly checked based on service and security requirements.
-  After cross-cluster mutual trust is configured, the KrbServer service needs to be restarted and the cluster becomes unavailable during the restart.
-  After cross-cluster mutual trust is configured, internal users **krbtgt/**\ *Local cluster domain name*\ **@**\ *External cluster domain name* and **krbtgt/**\ *External cluster domain name*\ **@**\ *Local cluster domain name* are added to the two clusters. The internal users cannot be deleted. For versions earlier than MRS 1.9.2, the default password is **Admin@123**, for MRS 1.9.2 or later, the default password is **Crossrealm@123**.

Procedure
---------

#. .. _mrs_01_0354__l0784aeae88934d19b78de6cb8fb5bbc4:

   On the MRS management console, query all security groups of the two clusters.

   -  If the security groups of the two clusters are the same, go to :ref:`3 <mrs_01_0354__l313690838fdd4efe880c73a525f3a5dc>`.
   -  If the security groups of the two clusters are different, go to :ref:`2 <mrs_01_0354__lebc29e3bd1dc48aea26ab1501ab7b5c6>`.

#. .. _mrs_01_0354__lebc29e3bd1dc48aea26ab1501ab7b5c6:

   On the VPC management console, add rules for each security group.

   Set **Protocol** to **ANY**, **Transfer Direction** to **Inbound**,

   and **Source** to **Security Group**. The source is the security group of the peer cluster.

   -  For cluster A, add inbound rules to the security group, set **Source** to the security groups of cluster B (the peer cluster of cluster A).
   -  For cluster B, add inbound rules to the security group, set **Source** to the security groups of cluster A (the peer cluster of cluster B).

   .. note::

      For a common cluster with Kerberos authentication disabled, perform step :ref:`1 <mrs_01_0354__l0784aeae88934d19b78de6cb8fb5bbc4>` to :ref:`2 <mrs_01_0354__lebc29e3bd1dc48aea26ab1501ab7b5c6>` to configure cross-cluster mutual trust. For a security cluster with Kerberos authentication enabled, after completing the preceding steps, proceed to the following steps for configuration.

#. .. _mrs_01_0354__l313690838fdd4efe880c73a525f3a5dc:

   Log in to MRS Manager of the two clusters separately. For details, see :ref:`Accessing MRS Manager MRS 2.1.0 or Earlier) <mrs_01_0102>`. Click **Service** and check whether the **Health Status** of all components is **Good**.

   -  If yes, go to :ref:`4 <mrs_01_0354__l2b421fc6a59b49f198148465895e2332>`.
   -  If no, contact technical support personnel for troubleshooting.

#. .. _mrs_01_0354__l2b421fc6a59b49f198148465895e2332:

   Query configuration information.

   a. On MRS Manager of the two clusters, choose **Services** > **KrbServer** > **Instance**. Query the **OM IP Address** of the two KerberosServer hosts.
   b. Click **Service Configuration**. Set **Type** to **All**. Choose **KerberosServer** > **Port** in the navigation tree on the left. Query the value of **kdc_ports**. The default value is **21732**.
   c. Click **Realm** and query the value of **default_realm**.

#. .. _mrs_01_0354__lf46908028ffa4276b982a3872741b63b:

   On MRS Manager of either cluster, modify the **peer_realms** parameter.

   .. table:: **Table 1** Parameter description

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                    |
      +===================================+================================================================================================================================================================================================================================================+
      | realm_name                        | Domain name of the mutual-trust cluster, that is, the value of **default_realm** obtained in step :ref:`4 <mrs_01_0354__l2b421fc6a59b49f198148465895e2332>`.                                                                                   |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | ip_port                           | KDC address of the peer cluster. Format: *IP address of a KerberosServer node in the peer cluster:kdc_port*                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                |
      |                                   | The addresses of the two KerberosServer nodes are separated by a comma. For example, if the IP addresses of the KerberosServer nodes are 10.0.0.1 and 10.0.0.2 respectively, the value of this parameter is **10.0.0.1:21732,10.0.0.2:21732**. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      -  To deploy trust relationships with multiple clusters, click |image1| to add items and specify relevant parameters. To delete an item, click |image2|.
      -  A cluster can have trust relationships with a maximum of 16 clusters. By default, no trust relationship exists between different clusters that are trusted by a local cluster.

#. Click **Save Configuration**. In the dialog box that is displayed, select **Restart the affected services or instances** and click **OK**. If you do not select **Restart the affected services or instances**, manually restart the affected services or instances.

   After **Operation successful** is displayed, click **Finish**.

#. .. _mrs_01_0354__l45679c1f701240a1bd1eaebbcc3ab4af:

   Exit MRS Manager and log in to it again. If the login is successful, the configurations are valid.

#. Log in to MRS Manager of the other cluster and repeat step :ref:`5 <mrs_01_0354__lf46908028ffa4276b982a3872741b63b>` to :ref:`7 <mrs_01_0354__l45679c1f701240a1bd1eaebbcc3ab4af>`.

Follow-up Operations
--------------------

After cross-cluster mutual trust is configured, the service configuration parameters are modified on MRS Manager and the service is restarted. Therefore, you need to prepare the client configuration file again and update the client.

Scenario 1:

Cluster A and cluster B (peer cluster and mutually trusted cluster) are the same type, for example, analysis cluster or streaming cluster. Follow instructions in :ref:`Updating a Client (Versions Earlier Than 3.x) <mrs_01_0089>` to update the client configuration files of cluster A and B respectively.

-  Update the client configuration file of cluster A.
-  Update the client configuration file of cluster B.

Scenario 2:

Cluster A and cluster B (peer cluster and mutually trusted cluster) are the different type. Perform the following steps to update the configuration files.

-  Update the client configuration file of cluster A to cluster B.
-  Update the client configuration file of cluster B to cluster A.
-  Update the client configuration file of cluster A.
-  Update the client configuration file of cluster B.

#. .. _mrs_01_0354__li26199321164818:

   Log in to MRS Manager of cluster A.

#. .. _mrs_01_0354__li25485761174241:

   Click **Services**, and then **Download Client**.

#. Set **Client Type** to **Only configuration files**.

#. Set **Download to** to **Remote host**.

#. Set **Host IP Address** to the IP address of the active Master node of cluster B, **Host Port** to 22, and **Save Path** to **/tmp**.

   -  If the default port **22** for logging in to cluster B using SSH is changed, set **Host Port** to a new port.
   -  The value of **Save Path** contains a maximum of 256 characters.

#. Set **Login User** to **root**.

   If another user is used, ensure that the user has permissions to read, write, and execute the save path.

#. In **SSH Private Key**, select and upload the key file used for creating cluster B.

#. Click **OK** to generate a client file.

   If the following information is displayed, the client file is saved. Click **Close**.

   .. code-block:: text

      Client files downloaded to the remote host successfully.

   If the following information is displayed, check the username, password, and security group configurations of the remote host. Ensure that the username and password are correct and an inbound rule of the SSH (22) port has been added to the security group of the remote host. And then, go to :ref:`2 <mrs_01_0354__li25485761174241>` to download the client again.

   .. code-block:: text

      Failed to connect to the server. Please check the network connection or parameter settings.

#. Log in to the ECS of cluster B using VNC. For details, see **Instances** > **Logging In to a Windows ECS > Login Using VNC** in the *Elastic Cloud Server User Guide*

   Log in to the ECS. For details, see `Login Using an SSH Key <https://docs.otc.t-systems.com/usermanual/ecs/en-us_topic_0017955380.html>`__. Set the ECS password and log in to the ECS in VNC mode.

#. Run the following command to switch to the client directory, for example, **/opt/Bigdata/client**:

   **cd /opt/Bigdata/client**

#. .. _mrs_01_0354__li1470645152711:

   Run the following command to update the client configuration of cluster A to cluster B:

   **sh refreshConfig.sh** *Client installation directory* *Full path of the client configuration file package*

   For example, run the following command:

   **sh refreshConfig.sh /opt/Bigdata/client /tmp/MRS_Services_Client.tar**

   If the following information is displayed, the configurations have been updated successfully.

   .. code-block::

      ReFresh components client config is complete.
      Succeed to refresh components client config.

   .. note::

      You can also refer to method 2 in :ref:`Updating a Client (Versions Earlier Than 3.x) <mrs_01_0089>` to perform operations in :ref:`1 <mrs_01_0354__li26199321164818>` to :ref:`11 <mrs_01_0354__li1470645152711>`.

#. Repeat step :ref:`1 <mrs_01_0354__li26199321164818>` to :ref:`11 <mrs_01_0354__li1470645152711>` to update the client configuration file of cluster B to cluster A.

#. Follow instructions in :ref:`Updating a Client (Versions Earlier Than 3.x) <mrs_01_0089>` to update the client configuration file of the local cluster.

   -  Update the client configuration file of cluster A.
   -  Update the client configuration file of cluster B.

.. |image1| image:: /_static/images/en-us_image_0000001296058048.jpg
.. |image2| image:: /_static/images/en-us_image_0000001349257345.jpg
