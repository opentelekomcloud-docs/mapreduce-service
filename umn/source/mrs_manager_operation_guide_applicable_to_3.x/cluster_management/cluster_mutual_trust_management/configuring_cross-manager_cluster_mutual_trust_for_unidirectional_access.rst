:original_name: admin_guide_000429.html

.. _admin_guide_000429:

Configuring Cross-Manager Cluster Mutual Trust for Unidirectional Access
========================================================================

Scenarios
---------

When the local cluster is in security mode and needs to access resources of another cluster in security mode (without restarting the cluster), you can configure unidirectional access with cross-cluster mutual trust by referring to this section so that users in the local cluster can be used in the peer system.

The secure usage scope of users in each system is referred to as a domain. Each MRS Manager must have a unique domain name. Cross-Manager access allows users to use resources across domains.

Notes and Constraints
---------------------

-  This section applies to MRS 3.6.0 or later.
-  A maximum of 500 mutually trusted clusters can be configured for a cluster.

Impact on the System
--------------------

-  After cross-Manager cluster mutual trust is configured, users of an external system can be used in the local system. The system administrator needs to periodically check the user permissions in Manager based on enterprise service and security requirements.
-  When cross-Manager cluster mutual trust is configured, all clusters need to be stopped, causing service interruptions.
-  After cross-Manager cluster mutual trust is configured, internal Kerberos users **krbtgt/**\ *Local cluster domain name*\ **@**\ *External cluster domain name* and **krbtgt/**\ *External cluster domain name*\ **@**\ *Local cluster domain name* are added to the two mutually trusted clusters. The internal users cannot be deleted. The system administrator needs to change the passwords periodically based on enterprise service and security requirements. The passwords of these four users in the two systems must be the same. For details, see :ref:`Changing the Password for a Component Running User <admin_guide_000257>`. When the passwords are changed, the connectivity between cross-cluster service applications may be affected.
-  After cross-Manager cluster mutual trust is configured, the clients of each cluster need to be downloaded and installed again.
-  After cross-Manager cluster mutual trust is configured, you need to check whether the system works properly and how to access resources of the peer system as a user of the local system. For details, see :ref:`Assigning User Permissions After Cross-Cluster Mutual Trust Is Configured <admin_guide_000178>`.

Prerequisites
-------------

-  The system administrator has clarified service requirements and planned domain names for the systems. A domain name can contain only uppercase letters, numbers, periods (.), and underscores (_), and must start with a letter or number.
-  The domain names of the two Managers are different. When an ECS or BMS cluster is created on MRS, a unique system domain name is randomly generated. Generally, you do not need to change the system domain name.
-  The two clusters do not have the same host name or the same IP address.
-  The system time of the two clusters is consistent, and the NTP services in the two systems use the same clock source.
-  The running status of all components in the Manager clusters is **Normal**.
-  The **acl.compare.shortName** parameter of the ZooKeeper service of all clusters in Manager is set to default value **true**. Otherwise, change the value to **true** and restart the ZooKeeper service.

Procedure
---------

#. Log in to the Manager of **the peer cluster** to be accessed by the local cluster.

#. .. _admin_guide_000429__en-us_topic_0000002187146341_l32a63fd5765949ef81b347d387df14fd:

   Choose **System** > **Permission** > **Domain and Mutual Trust**.

#. Modify **Peer Mutual Trust Domain**.

   .. table:: **Table 1** Related parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                       |
      +===================================+===================================================================================================================================================================================================================================================+
      | realm_name                        | Enter the domain name of the peer system.                                                                                                                                                                                                         |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | ip_port                           | Enter the KDC address of the peer system.                                                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                                                   |
      |                                   | The parameter value must follow the format *IP* *address:Port*.                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                                                                                   |
      |                                   | -  **IP address**: IP address of the node accommodating the Kerberos service in the peer system. To obtain the IP address, click the **Instances** tab on the KrbServer service page and check the service IP address of the KerberosServer role. |
      |                                   |                                                                                                                                                                                                                                                   |
      |                                   | -  **Port**: You can obtain the port number from the **kdc_ports** parameter of the KrbServer service. The default value is **21732**.                                                                                                            |
      |                                   |                                                                                                                                                                                                                                                   |
      |                                   |    For example, if the Kerberos service is deployed on nodes with IP addresses **10.0.0.1** and **10.0.0.2** that have established mutual trust with the local system, the parameter value is **10.0.0.1:21732,10.0.0.2:21732**.                  |
      |                                   |                                                                                                                                                                                                                                                   |
      |                                   | -  In dual-plane networking, enter the service plane IP address.                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                   |
      |                                   | -  If an IPv6 address is used, the IP address must be enclosed in square brackets ([]).                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                   |
      |                                   | -  Use commas (,) to separate the KDC addresses if the active and standby Kerberos services are deployed or multiple clusters in the peer system need to establish mutual trust with the local system.                                            |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      If you need to configure mutual trust for multiple MRS Manager systems, click to add a new item and set parameters. To delete unnecessary configurations, click .

#. .. _admin_guide_000429__en-us_topic_0000002187146341_en-us_topic_0046737083_li36527430:

   Click **OK**.

#. Log in to MRS Manager of the cluster and repeat :ref:`2 <admin_guide_000429__en-us_topic_0000002187146341_l32a63fd5765949ef81b347d387df14fd>` to :ref:`4 <admin_guide_000429__en-us_topic_0000002187146341_en-us_topic_0046737083_li36527430>`.

#. Log in to the active management node of the local cluster as user **omm**, and run the following command to update the domain configuration:

   **sh ${BIGDATA_HOME}/om-server/om/sbin/restart-RealmConfig.sh**

   The command is successfully executed if the following information is displayed:

   .. code-block::

      Modify realm successfully. Use the new password to log into FusionInsight again.

   After the restart, some hosts and services cannot be accessed and an alarm is generated. This problem can be automatically resolved in about 1 minute after **restart-RealmConfig.sh** is run.

#. Log in to the current cluster's MRS Manager and restart the cluster or instances with expired configurations.

   Confirm whether the Manager system domain name of this cluster has been modified.

   -  If the system domain name is changed, choose **More** > **Restart** in the upper right corner of the home page, enter the password, select the checkbox for confirming the impact, and click **OK**. Wait until the cluster is restarted.

   -  If the system domain name is not changed, choose **More** > **Restart Configuration-Expired Instances** in the upper right corner of the home page, enter the password, select the checkbox for confirming the impact, and click **OK**. Wait until the service is restarted.

      If the Doris service is installed in the cluster, choose **Cluster** > **Services** > **Doris**. On the **Dashboard** page, choose **More** > **Restart Service** in the upper right corner, enter the password, and click **OK**. Wait until the Doris service restarts.

#. Log out of MRS Manager and then log in again. If the login is successful, the configuration is successful.
