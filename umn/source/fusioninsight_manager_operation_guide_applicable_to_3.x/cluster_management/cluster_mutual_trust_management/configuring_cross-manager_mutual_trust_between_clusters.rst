:original_name: admin_guide_000177.html

.. _admin_guide_000177:

Configuring Cross-Manager Mutual Trust Between Clusters
=======================================================

Scenario
--------

When two security-mode clusters managed by different FusionInsight Managers need to access each other's resources, the system administrator can configure cross-Manager mutual trust for them.

The secure usage scope of users in each system is called a domain. Each FusionInsight Manager must have a unique domain name. Cross-Manager access allows users to use resources across domains.

.. note::

   A maximum of 500 mutually trusted clusters can be configured.

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

#. Log in to one FusionInsight Manager.

#. Stop all clusters on the home page.

   Click |image1| next to the target cluster and select **Stop**. Enter the password of the cluster administrator. In the **Stop Cluster** dialog box that is displayed, click **OK**. Wait until the cluster is stopped.

#. Choose **System** > **Permission** > **Domain and Mutual Trust**.

#. Modify **Peer Mutual Trust Domain**.

   .. table:: **Table 1** Related parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                   |
      +===================================+===============================================================================================================================================================================================================================================================================================================+
      | realm_name                        | Enter the domain name of the peer system.                                                                                                                                                                                                                                                                     |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | ip_port                           | Enter the KDC address of the peer system.                                                                                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | Value format: *IP address of the node accommodating the Kerberos service in the peer system:Port number*                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | -  In dual-plane networking, enter the service plane IP address.                                                                                                                                                                                                                                              |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | -  If an IPv6 address is used, the IP address must be enclosed in square brackets ([]).                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | -  Use commas (,) to separate the KDC addresses if the active and standby Kerberos services are deployed or multiple clusters in the peer system need to establish mutual trust with the local system.                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   | -  You can obtain the port number from the **kdc_ports** parameter of the KrbServer service. The default value is **21732**. To obtain the IP address of the node where the service is deployed, click the **Instance** tab on the KrbServer page and view **Service IP Address** of the KerberosServer role. |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   |    For example, if the Kerberos service is deployed on nodes at **10.0.0.1** and **10.0.0.2** that have established mutual trust with the local system, the parameter value is **10.0.0.1:21732,10.0.0.2:21732**.                                                                                             |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      If you need to configure mutual trust for multiple Managers, click |image2| to add a new item and set parameters. A maximum of 16 systems can be mutually trusted. Click |image3| to delete unnecessary configurations.

#. Click **OK**.

#. Log in to the active management node as user **omm**, and run the following command to update the domain configuration:

   **sh ${BIGDATA_HOME}/om-server/om/sbin/restart-RealmConfig.sh**

   The command is executed successfully if the following information is displayed:

   .. code-block::

      Modify realm successfully. Use the new password to log into FusionInsight again.

   After the restart, some hosts and services cannot be accessed and an alarm is generated. This problem can be automatically resolved in about 1 minute after **restart-RealmConfig.sh** is run.

#. Log in to FusionInsight Manager and start all clusters.

   Click |image4| next to the name of the target cluster and select **Start**. In the displayed **Start Cluster** dialog box, click **OK**. Wait until the cluster is started.

#. Log in to the other FusionInsight Manager and repeat the preceding operations.

.. |image1| image:: /_static/images/en-us_image_0278119935.png
.. |image2| image:: /_static/images/en-us_image_0263899403.png
.. |image3| image:: /_static/images/en-us_image_0263899531.png
.. |image4| image:: /_static/images/en-us_image_0263899495.png
