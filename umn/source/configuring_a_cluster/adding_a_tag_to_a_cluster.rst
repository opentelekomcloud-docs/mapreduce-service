:original_name: mrs_01_0048.html

.. _mrs_01_0048:

Adding a Tag to a Cluster
=========================

Tags are used to identify clusters. Adding tags to clusters can help you identify and manage your cluster resources.

You can add a maximum of 10 tags to a cluster when creating the cluster or add them on the details page of the created cluster.

A tag consists of a tag key and a tag value. :ref:`Table 1 <mrs_01_0048__t7d9a642e3af04b229bf4e8f93954f3ad>` provides tag key and value requirements.

.. _mrs_01_0048__t7d9a642e3af04b229bf4e8f93954f3ad:

.. table:: **Table 1** Tag key and value requirements

   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Requirement                                                                                                                 | Example               |
   +=======================+=============================================================================================================================+=======================+
   | Key                   | A tag key cannot be left blank.                                                                                             | Organization          |
   |                       |                                                                                                                             |                       |
   |                       | A tag key must be unique in a cluster.                                                                                      |                       |
   |                       |                                                                                                                             |                       |
   |                       | A tag key contains a maximum of 36 characters.                                                                              |                       |
   |                       |                                                                                                                             |                       |
   |                       | A tag value cannot contain special characters ``(=*<>\,|/)`` or start or end with spaces.                                   |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Value                 | A tag value contains a maximum of 43 characters.                                                                            | Apache                |
   |                       |                                                                                                                             |                       |
   |                       | A tag value cannot contain special characters ``(=*<>\,|/)`` or start or end with spaces. This parameter can be left blank. |                       |
   +-----------------------+-----------------------------------------------------------------------------------------------------------------------------+-----------------------+

Adding Tags to a Cluster
------------------------

You can perform the following operations to add tags to a cluster when creating the cluster.

#. Log in to the MRS console.

#. Click **Create** **Cluster**. The corresponding page is displayed.

#. Click the **Custom Config** tab.

#. Configure the cluster software and hardware by referring to :ref:`Creating a Custom Cluster <mrs_01_0513>`.

#. On the **Set Advanced Options** tab page, add a tag.

   Enter the key and value of a tag to be added.

   You can add a maximum of 10 tags to a cluster and use intersections of tags to search for the target cluster.

   .. note::

      You can also add tags to existing clusters. For details, see :ref:`Managing Tags <mrs_01_0048__section188067265123>`.

Searching for the Target Cluster
--------------------------------

On the **Active Clusters** page, search for the target cluster by tag key or tag value.

#. Log in to the MRS console.

#. In the upper right corner of the **Active Clusters** page, click **Search by Tag** to access the search page.

#. Enter the tag of the cluster to be searched.

   You can select a tag key or tag value from their drop-down lists. When the tag key or tag value is exactly matched, the system can automatically locate the target cluster. If you enter multiple tags, their intersections are used to search for the cluster.

#. Click **Search**.

   The system searches for the target cluster by tag key or value.

.. _mrs_01_0048__section188067265123:

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
