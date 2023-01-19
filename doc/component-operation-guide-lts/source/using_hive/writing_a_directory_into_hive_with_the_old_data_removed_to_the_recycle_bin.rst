:original_name: mrs_01_0967.html

.. _mrs_01_0967:

Writing a Directory into Hive with the Old Data Removed to the Recycle Bin
==========================================================================

Scenario
--------

This function applies to Hive.

After this function is enabled, run the following command to write a directory into Hive: **insert overwrite directory "**\ */path1*\ **"** **...**. After the operation is successfully performed, the old data is removed to the recycle bin, and the directory cannot be an existing database path in the Hive metastore.

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **Hive** > **Configurations** > **All Configurations**.
#. Choose **HiveServer(Role)** > **Customization**, add a customized parameter to the **hive-site.xml** parameter file, set **Name** to **hive.overwrite.directory.move.trash**, and set **Value** to **true**. Restart all Hive instances after the modification.
