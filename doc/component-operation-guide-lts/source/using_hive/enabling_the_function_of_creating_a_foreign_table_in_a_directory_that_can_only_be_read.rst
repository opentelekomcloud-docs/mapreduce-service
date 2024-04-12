:original_name: mrs_01_0971.html

.. _mrs_01_0971:

Enabling the Function of Creating a Foreign Table in a Directory That Can Only Be Read
======================================================================================

Scenario
--------

This function is applicable to Hive and Spark2x.

After this function is enabled, the user or user group that has the read and execute permissions on a directory can create foreign tables in the directory without checking whether the current user is the owner of the directory. In addition, the directory of a foreign table cannot be stored in the default directory **\\warehouse**. In addition, do not change the permission of the directory during foreign table authorization.

.. note::

   After this function is enabled, the function of the foreign table changes greatly. Based on the actual application scenario, determine whether to enable this function.

Procedure
---------

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **Hive** > **Configurations** > **All Configurations**.
#. Modify parameters and restart related instances:

   -  For versions earlier than MRS 3.2.0:

      a. Choose **MetaStore(Role)** > **Customization**, add a custom parameter to the **hivemetastore-site.xml** parameter file, and set **Name** to **hive.supports.over.32.roles** and **Value** to **true**.
      b. Choose **HiveServer(Role)** > **Customization** for versions earlier than MRS 3.2.0, add a custom parameter to the **hive-site.xml** parameter file, set **Name** to **hive.supports.over.32.roles**, and set **Value** to **true**.
      c. Click **Save** to save the configuration.
      d. Click **Instance**, select all Hive instances, and choose **More** > **Restart** Instance to restart all Hive instances.

   -  For MRS 3.2.0 or later:

      a. Choose **MetaStore(Role)** > **Customization**, add a custom parameter to the **hivemetastore-site.xml** parameter file, and set **Name** to **hive.supports.over.32.roles** and **Value** to **true**.
      b. Click **Save** to save the configuration.
      c. Click **Instance**, select all MetaStore instances, and choose **More** > **Restart** Instance to restart all MetaStore instances.
