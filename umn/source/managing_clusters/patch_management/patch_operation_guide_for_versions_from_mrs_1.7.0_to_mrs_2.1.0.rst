:original_name: mrs_01_0411.html

.. _mrs_01_0411:

Patch Operation Guide for Versions from MRS 1.7.0 to MRS 2.1.0
==============================================================

If you obtain patch information from the following sources, upgrade the patch according to actual requirements.

-  You obtain information about the patch released by MRS from a message pushed by the message center service.
-  You obtain information about the patch by accessing the cluster and viewing patch information.

Preparing for Patch Installation
--------------------------------

-  Follow instructions in :ref:`Performing a Health Check <mrs_01_0224>` to check cluster status. If the cluster health status is normal, install a patch.
-  You need to confirm the target patch to be installed according to the patch information in the patch content.

Installing a Patch
------------------

#. Log in to the MRS console.
#. Choose **Clusters > Active Clusters** and click the name of the cluster to be queried to enter the page displaying the cluster's basic information.
#. On the **Patches** tab page, click **Install** in the **Operation** column to install the target patch.

   .. note::

      -  Clusters of versions later than MRS 1.7.2 support rolling patch installation. For details, see :ref:`Rolling Patches <mrs_01_0431>`.
      -  For the isolated host nodes in the cluster, follow instructions in :ref:`Restoring Patches for the Isolated Hosts <mrs_01_0412>` to restore the patch.

Uninstalling a Patch
--------------------

#. Log in to the MRS console.
#. Choose **Clusters > Active Clusters** and click the name of the cluster to be queried to enter the page displaying the cluster's basic information.
#. On the **Patches** page, click **Uninstall** in the **Operation** column to uninstall the target patch.

   .. note::

      -  Clusters of versions later than MRS 1.7.2 support rolling patch installation. For details, see :ref:`Rolling Patches <mrs_01_0431>`.
      -  For the isolated host nodes in the cluster, follow instructions in :ref:`Restoring Patches for the Isolated Hosts <mrs_01_0412>` to restore the patch.
