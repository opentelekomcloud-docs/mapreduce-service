:original_name: admin_guide_000415.html

.. _admin_guide_000415:

Switching Ranger Authentication
===============================

Scenario
--------

By default, the Ranger service is installed and Ranger authentication is enabled for a newly installed cluster in security mode. You can set fine-grained security access policies for accessing component resources through the permission plug-in of the component. If Ranger authentication is not required, the cluster administrator can manually disable Ranger authentication on the service page. After Ranger authentication is disabled, the system continues to perform permission control based on the role model of FusionInsight Manager when accessing component resources.

In a cluster upgraded from an earlier version, Ranger authentication is not used by default when users access component resources. The cluster administrator can manually enable Ranger authentication after installing the Ranger service.

.. note::

   -  In a cluster in security mode, the following components support Ranger authentication: HDFS, YARN, Kafka, Hive, HBase, Storm,, Impala, and Spark2x.
   -  In a cluster in non-security mode, Ranger supports permission control on component resources based on OS users. The following components support Ranger authentication: HBase, HDFS, Hive, Spark2x, and YARN.
   -  After Ranger authentication is enabled, all authentication of the component will be managed by Ranger. The permissions set by the original authentication plug-in will become invalid (The ACL rules of HDFS and YARN components still take effect). Exercise caution when performing this operation. You are advised to deploy permissions on Ranger in advance.
   -  After Ranger authentication is disabled, all authentication of the component will be managed by the permission plug-in of the component. The permission set on Ranger will become invalid. Exercise caution when performing this operation. You are advised to deploy permissions on Manager in advance.

Enabling Ranger Authentication
------------------------------

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > **Services**.
#. Click the specified service name on the service management page.
#. On the service details page, expand the **More** drop-down list and select **Enable Ranger**.
#. In the displayed dialog box, enter the password of the current login user and click **OK**.
#. In the service list, restart the service whose configuration has expired.

Disabling Ranger Authentication
-------------------------------

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > **Services**.
#. Click the specified service name on the service management page.
#. On the service details page, expand the **More** drop-down list and select **Disable Ranger**.
#. Enter the password of the current login user and click **OK**. In the displayed dialog box, click **OK**.
#. In the service list, restart the service whose configuration has expired.
