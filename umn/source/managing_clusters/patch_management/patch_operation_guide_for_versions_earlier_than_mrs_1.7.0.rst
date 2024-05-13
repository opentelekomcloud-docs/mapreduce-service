:original_name: mrs_01_0410.html

.. _mrs_01_0410:

Patch Operation Guide for Versions Earlier than MRS 1.7.0
=========================================================

If you obtain patch information from the following sources, upgrade the patch according to actual requirements.

-  You obtain information about the patch released by MRS from a message pushed by the message center service.
-  You obtain information about the patch by accessing the cluster and viewing patch information.

Preparing for Patch Installation
--------------------------------

-  Follow instructions in :ref:`Performing a Health Check <mrs_01_0224>` to check cluster status. If the cluster health status is normal, install a patch.
-  The administrator has uploaded the cluster patch package to the server. For details, see :ref:`Uploading a Patch Package <mrs_01_0410__section63677183610>`.
-  You need to confirm the target patch to be installed according to the patch information in the patch content.

.. _mrs_01_0410__section63677183610:

Uploading a Patch Package
-------------------------

#. Access MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`.
#. Choose **System > Manage Patch**. The **Manage Patch** page is displayed.
#. Click **Upload Patch** and set the following parameters.

   -  **Patch File Path**: folder created in the OBS file system where the patch package is stored, for example, **MRS_1.6.2/MRS_1_6_2_11.tar.gz**
   -  **Parallel File System Name**: name of the OBS file system that stores patch packages, for example, **mrs_patch**.

      .. note::

         You can obtain the file system name and patch file path on the **Patch Information** tab page. The value of the **Patch Path** is in the following format: *[File system name]*\ **/**\ *[Patch file path]*.

   -  **AK**: For details, see **My Credential** > **Access Keys**.
   -  **SK**: For details, see **My Credential** > **Access Keys**.

#. Click **OK** to upload the patch.

Installing a Patch
------------------

#. Access MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`.
#. Choose **System > Manage Patch**. The **Manage Patch** page is displayed.
#. In the **Operation** column, click **Install**.
#. In the displayed dialog box, click **OK** to install the patch.
#. After the patch is installed, you can view the installation status in the progress bar. If the installation fails, contact the administrator.

   .. note::

      For the isolated host nodes in the cluster, follow instructions in :ref:`Restoring Patches for the Isolated Hosts <mrs_01_0412>` to restore the patch.

Uninstalling a Patch
--------------------

#. Access MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`.
#. Choose **System > Manage Patch**. The **Manage Patch** page is displayed.
#. In the **Operation** column, click **Uninstall**.

   .. note::

      For the isolated host nodes in the cluster, follow instructions in :ref:`Restoring Patches for the Isolated Hosts <mrs_01_0412>` to restore the patch.
