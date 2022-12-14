:original_name: mrs_01_0974.html

.. _mrs_01_0974:

HiveServer Lease Isolation
==========================

Scenario
--------

-  This function applies to Hive.
-  This function can be enabled to specify specific users to access HiveServer services on specific nodes, achieving HiveServer resource isolation.

.. note::

   This section applies to MRS 3.\ *x* or later clusters.

Procedure
---------

This section describes how to set lease isolation for user **hiveuser** for existing HiveServer instances.

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`.

#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **HiveServer**.

#. In the HiveServer list, select the HiveServer for which lease isolation is configured and choose **HiveServer** > **Instance Configurations** > **All Configurations**.

#. .. _mrs_01_0974__li21663526200:

   In the upper right corner of the **All Configurations** page, search for **hive.server2.zookeeper.namespace** and specify its value, for example, **hiveserver2_zk**.

#. Click **Save**. In the dialog box that is displayed, click **OK**.

#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive**, choose **More** > **Restart Service**, and enter the password to restart the service.

#. Run the **beeline -u** command to log in to the client and run the following command:

   **beeline -u "jdbc:hive2://**\ *10.5.159.13*\ **:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=**\ *hiveserver2\_zk*\ **;sasl.qop=auth-conf;auth=KERBEROS;principal=hive/hadoop.**\ *<System domain name*\ **>@**\ *<System domain name>*\ **"**

   In the command, **10.5.159.13** is replaced with the IP address of any ZooKeeper instance, which can be viewed through **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper** > **Instance**.

   **hiveserver2_zk** following **zooKeeperNamespace=** is set to the value of **hive.server2.zookeeper.namespace** in :ref:`4 <mrs_01_0974__li21663526200>`.

   As a result, only the HiveServer whose lease isolation is configured can be logged in.

   .. note::

      -  After this function is enabled, you must run the preceding command during login to access the HiveServer for which lease isolation is configured. If you run the **beeline** command to log in to the client, only the HiveServer that is not isolated by the lease is accessed.
      -  You can log in to FusionInsight Manager, choose **System** > **Permission** > **Domain and Mutual Trust**, and view the value of **Local Domain**, which is the current system domain name. **hive/hadoop.**\ <*system domain name*> is the username. All letters in the system domain name contained in the username are lowercase letters.
