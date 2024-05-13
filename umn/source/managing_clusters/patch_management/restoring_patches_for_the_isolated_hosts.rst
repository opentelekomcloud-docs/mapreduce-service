:original_name: mrs_01_0412.html

.. _mrs_01_0412:

Restoring Patches for the Isolated Hosts
========================================

If some hosts are isolated in a cluster, perform the following operations to restore patches for these isolated hosts after patch installation on other hosts in the cluster. After patch restoration, versions of the isolated host nodes are consistent with those are not isolated.

.. note::

   In **MRS 3.x**, you cannot perform operations in this section on the management console.

#. Access MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`.
#. Choose **System > Manage Patch**. The **Manage Patch** page is displayed.
#. In the **Operation** column, click **View Details**.
#. On the patch details page, select host nodes whose **Status** is **Isolated**.
#. Click **Select and Restore** to restore the isolated host nodes.
