:original_name: mrs_01_2493109.html

.. _mrs_01_2493109:

How Do I Handle Abnormal Status of Core Nodes in an MRS Cluster After Successful Expansion?
===========================================================================================

Symptom
-------

Cores nodes are added, but some instances on the nodes may fail to be started. The symptoms are as follows:

#. A core node has been added and is displayed on the **Nodes** page.

#. Some tasks for adding nodes fail or are partially successful.

   |image1|

#. If IAM users have been synchronized, you can view unstarted roles on the **Components** page.

#. If they are not synchronized, you can view unstarted roles on the Manager page of this cluster.

Handling Core Node Anomaly After Capacity Expansion
---------------------------------------------------

Scenario 1: The task for adding nodes fails before component installation.

#. Perform the following steps if the MRS cluster is a pay-per-use cluster:

   a. Log in to the MRS console.

   b. Choose **Active Clusters** and click the name of a cluster to access its details page.

   c. Click |image2| in the upper part of the page. In the **Task List** column, click the task for adding core nodes.

   d. .. _mrs_01_2493109__en-us_topic_0000001925619617_en-us_topic_0000001884788385_li337917341517:

      Records all nodes in the verification request parameter.

   e. Click the **Nodes** tab, select the nodes recorded in :ref:`1.d <mrs_01_2493109__en-us_topic_0000001925619617_en-us_topic_0000001884788385_li337917341517>`, click **Stop** in the upper right corner, and stop the nodes as prompted.

   f. Reduce nodes.

Scenario 2: The task for adding nodes fails after component installation.

#. Log in to the MRS console.
#. Choose **Active Clusters** and click the name of a cluster to access its details page.
#. On the **Dashboard** tab, click **Synchronize** next to **IAM User Sync** to synchronize IAM users.
#. Click **Components** and check the role status of each service. If a role is not started, select the role, click **More**, and select **Start Instance** to start the instance.
#. If the startup fails, rectify the fault based on the error information in the task list and try again.

   -  If many roles are abnormal, click **Management Operations** in the upper right corner to start all components.
   -  For other exceptions that cannot be resolved, contact technical support.
   -  You can also start the instance on MRS Manager.

.. |image1| image:: /_static/images/en-us_image_0000002757184459.png
.. |image2| image:: /_static/images/en-us_image_0000002757263961.png
