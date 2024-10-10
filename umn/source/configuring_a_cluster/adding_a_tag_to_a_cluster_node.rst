:original_name: mrs_01_0048.html

.. _mrs_01_0048:

Adding a Tag to a Cluster/Node
==============================

Tags are used to identify clusters/nodes. Adding tags to clusters can help you identify and manage your cluster resources.

-  Cluster tags: You can add up to 10 tags to a cluster during cluster creation or add them on the details page of a created cluster. Updating a cluster tag will synchronize the tag to all nodes in the cluster.

-  Node tags: You can use the default tag or add tags to nodes in an MRS cluster when you configure an auto scaling policy. Node tags take the tag quotas. You can view the tags of a node in the **Nodes** tab on MRS console.

-  Default tags: An MRS cluster contains multiple nodes, and each node is an ECS and contains EVS disks. After the default tag is enabled, the system automatically creates a cluster tag and a tag for each node. The default tag is automatically synchronized to the corresponding ECS or EVS instances.

   To view node tags, go to the **Nodes** tab on the MRS console, and move the cursor to the tag icon of a node in the node list.

   .. note::

      -  MRS tag updates are synchronized to the ECSs or EVS disks in the cluster. However, if you modify MRS cluster tags on the ECS or EVS console, the modification will not be synchronized to MRS. To ensure tag consistency, do not modify MRS cluster tags on the ECS or EVS console.
      -  You can add a maximum of 10 tags to a cluster. If the number of tags of a node in the cluster reaches the upper limit, no more tags can be added to the cluster.
      -  If default tags are enabled, a default tag is added to the cluster and each node, which takes two quotas. That is, a maximum of 10 tags can be added by default. In this case, a maximum of eight more tags can still be added.

If your organization has configured tag strategies for MRS, add tags to clusters/nodes based on the strategies. If a tag does not comply with the tag strategies, the cluster/node may be failed to be created. Contact the organization administrator to learn more about the tag strategies.

A tag consists of a tag key and a tag value. :ref:`Table 1 <mrs_01_0048__t7d9a642e3af04b229bf4e8f93954f3ad>` provides tag key and value requirements.

.. _mrs_01_0048__t7d9a642e3af04b229bf4e8f93954f3ad:

.. table:: **Table 1** Tag key and value requirements

   +-----------------------+------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Requirement                                                                                                                  | Example               |
   +=======================+==============================================================================================================================+=======================+
   | Key                   | A tag key cannot be left blank.                                                                                              | Organization          |
   |                       |                                                                                                                              |                       |
   |                       | A tag key must be unique in a cluster.                                                                                       |                       |
   |                       |                                                                                                                              |                       |
   |                       | A tag key contains a maximum of 36 characters.                                                                               |                       |
   |                       |                                                                                                                              |                       |
   |                       | A tag value cannot contain special characters\ ``(=*<>\,|/)`` or start or end with spaces.                                   |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Value                 | A tag value contains a maximum of 43 characters.                                                                             | Apache                |
   |                       |                                                                                                                              |                       |
   |                       | A tag value cannot contain special characters\ ``(=*<>\,|/)`` or start or end with spaces. This parameter can be left blank. |                       |
   +-----------------------+------------------------------------------------------------------------------------------------------------------------------+-----------------------+

Adding Tags to a Cluster
------------------------

-  Adding cluster tags during cluster creation

   #. Log in to the MRS console.
   #. Click **Create** **Cluster**. The page for creating a cluster is displayed.
   #. Click the **Custom Config** tab.
   #. Configure the cluster software and hardware by referring to :ref:`Creating a Custom Cluster <mrs_01_0513>`.
   #. Select **Configure** on the right of **Set Advanced Options** and enter the key and value of a new tag.

-  .. _mrs_01_0048__li1665012143912:

   Adding tags to an existing cluster

   #. Log in to the MRS management console.
   #. In the navigation pane on the left, choose **Active Clusters**. Click the name of a running cluster. The basic information page of the cluster is displayed.
   #. Click the **Tags** tab.
   #. Click **Add/Edit Tag**. If this is your first time adding a tag, click **Add Tag**. In the displayed dialog box, enter the key and value of a tag, and click **Add**.

      .. note::

         You can also add cluster tags by enabling default tags. All nodes will be tagged with the cluster ID and node IDs, which takes two quotas.

   #. Click **OK**.

Adding Tags to a Node
---------------------

-  Node tags are automatically added when a default tag is added to a cluster. For details, see :ref:`Adding tags to an existing cluster <mrs_01_0048__li1665012143912>`.

-  Adding node tags for auto scaling

   If you add a tag when configuring an auto scaling policy, MRS automatically adds the tag to the new nodes and synchronizes the tag to the ECSs and EVS disks.

   #. Log in to the MRS management console.
   #. In the navigation pane on the left, choose **Active Clusters**. Click the name of a running cluster. The basic information page of the cluster is displayed.
   #. On the page that is displayed, click the **Auto Scaling** tab.
   #. Click **Edit** on the right of an existing auto scaling policy. In the displayed dialog box, enter the key and value of the tag you want to add, and click **Add**.

      .. note::

         -  You need to enable the auto scaling policy and configure scale-out rules. Otherwise, the node tags will not take effect.
         -  If tag quotas are insufficient, delete the cluster tag or modify existing a tag of the auto scaling policy, and then enable the policy.
         -  Tags cannot be added to auto scaling policies of resource pools.

   #. Click **OK**.

Searching for the Target Cluster
--------------------------------

On the **Active Clusters** page, search for the target cluster by tag key or tag value.

#. Log in to the MRS console.

#. In the upper right corner of the **Active Clusters** page, click **Search by Tag** to access the search page.

#. Enter the tag of the cluster to be searched.

   You can select a tag key or tag value from their drop-down lists. When the tag key or tag value is exactly matched, the system can automatically locate the target cluster. If you enter multiple tags, their intersections are used to search for the cluster.

#. Click **Search**.

   The system searches for the target cluster by tag key or value.

Managing Tags
-------------

You can view, add, modify, and delete tags on the **Tags** tab page of the cluster.

#. Log in to the MRS console.

#. On the **Active Clusters** page, click the name of a cluster for which you want to manage tags.

   The cluster details page is displayed.

#. Click the **Tags** tab and view, add, modify, and delete tags on the tab page.

   -  View

      On the **Tags** tab page, you can view details about tags of the cluster, including the number of tags and the key and value of each tag.

   -  Add

      Click **Add Tag** in the upper left corner. In the displayed **Add Tag** dialog box, enter the key and value of the tag to be added, and click **OK**.

   -  Modify

      In the **Operation** column of the tag, click **Edit**. In the displayed **Edit Tag** page, enter new tag key and value and click **OK**.

   -  Delete

      In the **Operation** column of the tag, click **Delete**. After confirmation, click **OK** in the displayed page for deleting a tag.

      .. note::

         MRS cluster tag updates will be synchronized to every ECS in the cluster. You are advised not to modify ECS tags on the ECS console to prevent inconsistency between ECS tags and MRS cluster tags. If the number of tags of an ECS in the MRS cluster reaches the upper limit, you cannot create any tag for the MRS cluster.
