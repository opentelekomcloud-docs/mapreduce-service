:original_name: mrs_01_0355.html

.. _mrs_01_0355:

Configuring Users to Access Resources of a Trusted Cluster
==========================================================

Scenario
--------

After cross-cluster mutual trust is configured, permission must be configured for users in the local cluster, so that the users can access the same resources in the peer cluster as the users in the peer cluster.

.. note::

   The operations described in this section apply only to clusters of versions earlier than MRS 3.x.

   For clusters of **MRS 3.\ x** or later, see :ref:`Assigning User Permissions After Cross-Cluster Mutual Trust Is Configured <admin_guide_000178>`.

Prerequisites
-------------

The mutual trust relationship has been configured between two clusters (clusters A and B). The clients of the clusters have been updated.

Procedure
---------

#. Log in to MRS Manager of cluster A and choose **System** > **Manage User**. Check whether cluster A has accounts that are the same as those of cluster B.

   -  If yes, go to :ref:`2 <mrs_01_0355__l3a44878c05474ed09661e8c1b21018df>`.
   -  If no, go to :ref:`3 <mrs_01_0355__l818dc8bf23ba4e23a260eb70945d47c2>`.

#. .. _mrs_01_0355__l3a44878c05474ed09661e8c1b21018df:

   Click |image1| on the left side of the username to unfold the detailed user information. Check whether the user group and role to which the user belongs meet the service requirements.

   For example, user **admin** of cluster A has the permission to access and create files in the **/tmp** directory of cluster A. Then go to :ref:`4 <mrs_01_0355__l9137cfca08bf4e63a5eb91f29a64a9c9>`.

#. .. _mrs_01_0355__l818dc8bf23ba4e23a260eb70945d47c2:

   Create the accounts in cluster A and bind the accounts to the user group and roles required by the services. Then go to :ref:`4 <mrs_01_0355__l9137cfca08bf4e63a5eb91f29a64a9c9>`.

#. .. _mrs_01_0355__l9137cfca08bf4e63a5eb91f29a64a9c9:

   Choose **Service** > **HDFS** > **Instance**. Query the **OM IP Address** of **NameNode (Active)**.

#. Log in to the client of cluster B.

   For example, if you have updated the client on the Master2 node, log in to the Master2 node to use the client. For details, see :ref:`Using an MRS Client <mrs_01_0088>`.

#. Run the following command to access the **/tmp** directory of cluster A.

   **hdfs dfs -ls hdfs://192.168.6.159:9820/tmp**

   In the preceding command, **192.168.6.159** is the IP address of the active NameNode of cluster A; **9820** is the default port for communication between the client and the NameNode.

   .. note::

      For MRS 1.6.2 or earlier, the default port number is **25000**. For details, see :ref:`List of Open Source Component Ports <mrs_01_0504>`.

#. Run the following command to create a file in the **/tmp** directory of cluster A:

   **hdfs dfs -touchz hdfs://192.168.6.159:9820/tmp/mrstest.txt**

   If you can query the **mrstest.txt** file in the **/tmp** directory of cluster A, the cross-cluster mutual trust is configured successfully.

.. |image1| image:: /_static/images/en-us_image_0000001349137821.png
