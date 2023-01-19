:original_name: mrs_01_0966.html

.. _mrs_01_0966:

Viewing Table Structures Using the show create Statement as Users with the select Permission
============================================================================================

Scenario
--------

This function is applicable to Hive and Spark2x in.

With this function enabled, if the select permission is granted to a user during Hive table creation, the user can run the **show create table** command to view the table structure.

Procedure
---------

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **Hive** > **Configurations** > **All Configurations**.
#. Choose **HiveServer(Role)** > **Customization**, add a customized parameter to the **hive-site.xml** parameter file, set **Name** to **hive.allow.show.create.table.in.select.nogrant**, and set **Value** to **true**. Restart all Hive instances after the modification.
#. Determine whether to enable this function on the Spark2x client.

   -  If yes, download and install the Spark2x client again.
   -  If no, no further action is required.
