:original_name: mrs_01_0968.html

.. _mrs_01_0968:

Inserting Data to a Directory That Does Not Exist
=================================================

Scenario
--------

This function applies to Hive.

With this function enabled, run the **insert overwrite directory** */path1/path2/path3*... command to write a subdirectory. The permission of the */path1/path2* directory is 700, and the owner is the current user. If the */path3* directory does not exist, it is automatically created and data is written successfully.

This function is supported when **hive.server2.enable.doAs** is set to **true** in earlier versions. This version supports the function when **hive.server2.enable.doAs** is set to **false**.

.. note::

   The parameter adjustment of this function is the same as that of the custom parameters added in :ref:`Writing a Directory into Hive with the Old Data Removed to the Recycle Bin <mrs_01_0967>`.

Procedure
---------

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **Hive** > **Configurations** > **All Configurations**.
#. Choose **HiveServer(Role)** > **Customization**, add a customized parameter to the **hive-site.xml** parameter file, set **Name** to **hive.overwrite.directory.move.trash**, and set **Value** to **true**. Restart all Hive instances after the modification.
