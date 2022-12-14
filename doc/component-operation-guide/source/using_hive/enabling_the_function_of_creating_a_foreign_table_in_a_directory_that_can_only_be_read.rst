:original_name: mrs_01_0971.html

.. _mrs_01_0971:

Enabling the Function of Creating a Foreign Table in a Directory That Can Only Be Read
======================================================================================

Scenario
--------

This function is applicable to Hive and Spark2x for MRS 3.\ *x* or later, or Hive and Spark for versions earlier than MRS 3.x.

After this function is enabled, the user or user group that has the read and execute permissions on a directory can create foreign tables in the directory without checking whether the current user is the owner of the directory. In addition, the directory of a foreign table cannot be stored in the default directory **\\warehouse**. In addition, do not change the permission of the directory during foreign table authorization.

.. note::

   After this function is enabled, the function of the foreign table changes greatly. Based on the actual application scenario, determine whether to enable this function.

Procedure
---------

#. The Hive service configuration page is displayed.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager, choose **Services** > **Hive** > **Service Configuration**, and select **All** from the **Basic** drop-down list.
   -  For MRS 1.9.2 or later, click the cluster name on the MRS console, choose **Components** > **Hive** > **Service Configuration**, and select **All** from the **Basic** drop-down list.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   -  For MRS 3.\ *x* or later, log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. And choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Configurations** > **All Configurations**.

#. Choose **HiveServer(Role)** > **Customization**, add a customized parameter to the **hive-site.xml** parameter file, set **Name** to **hive.restrict.create.grant.external.table**, and set **Value** to **true**.
#. Choose **MetaStore(Role)** > **Customization**, add a customized parameter to the **hivemetastore-site.xml** parameter file, set **Name** to **hive.restrict.create.grant.external.table**, and set **Value** to **true**. Restart all Hive instances after the modification.
#. Determine whether to enable this function on the Spark/Spark2x client.

   -  If yes, download and install the Spark/Spark2x client again.
   -  If no, no further action is required.
