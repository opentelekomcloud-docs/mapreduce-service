:original_name: mrs_01_0970.html

.. _mrs_01_0970:

Disabling of Specifying the location Keyword When Creating an Internal Hive Table
=================================================================================

Scenario
--------

This function is applicable to Hive and Spark2x.

After this function is enabled, the **location** keyword cannot be specified when a Hive internal table is created. Specifically, after a table is created, the table path following the location keyword is created in the default **\\warehouse** directory and cannot be specified to another directory. If the location is specified when the internal table is created, the creation fails.

.. note::

   After this function is enabled, the location keyword cannot be specified during the creation of a Hive internal table. The table creation statement is restricted. If a table that has been created in the database is not stored in the default directory **/warehouse**, the **location** keyword can still be specified when the database creation, table script migration, or metadata recreation operation is performed by disabling this function temporarily.

Procedure
---------

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **Hive** > **Configurations** > **All Configurations**.
#. Choose **HiveServer(Role)** > **Customization**, add a customized parameter to the **hive-site.xml** parameter file, set **Name** to **hive.internaltable.notallowlocation**, and set **Value** to **true**. Restart all Hive instances after the modification.
#. Determine whether to enable this function on the Spark2x client.

   -  If yes, download and install the Spark2x client again.
   -  If no, no further action is required.
