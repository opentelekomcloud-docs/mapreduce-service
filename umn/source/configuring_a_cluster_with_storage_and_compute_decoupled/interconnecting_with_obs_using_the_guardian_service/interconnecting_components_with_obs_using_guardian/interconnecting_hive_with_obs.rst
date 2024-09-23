:original_name: mrs_01_248989.html

.. _mrs_01_248989:

Interconnecting Hive with OBS
=============================

.. _mrs_01_248989__en-us_topic_0000001656985526_section18127143141811:

Interconnecting with OBS
------------------------

MRS clusters allow Hive to connect to OBS through Metastore.

Interconnecting Hive with OBS through Metastore

#. You have configured storage and compute decoupling by referring to :ref:`Interconnecting the Guardian Service with OBS <mrs_01_248978>`.

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Hive**, and click **Configurations**.

#. Search for **hive.metastore.warehouse.dir** in the search box and change the parameter value to an OBS path, for example, **obs://hivetest/user/hive/warehouse/**. **hivetest** indicates the OBS file system name.


   .. figure:: /_static/images/en-us_image_0000001973053750.png
      :alt: **Figure 1** hive.metastore.warehouse.dir configuration

      **Figure 1** hive.metastore.warehouse.dir configuration

#. Save the configuration, choose **Cluster** > **Services**, and restart the Hive service in the service list.

#. Update the client configuration file.

   a. Log in to the node where the Hive client is located and run the following command to modify **hivemetastore-site.xml** in the Hive client configuration file directory:

      **vi** *Client installation directory*\ **/Hive/config/hivemetastore-site.xml**

   b. Change the value of **hive.metastore.warehouse.dir** to the corresponding OBS path, for example, **obs://hivetest/user/hive/warehouse/**.

      |image1|

   c. Change the value of **hive.metastore.warehouse.dir** of **hivemetastore-site.xml** in the HCatalog client configuration file directory to the corresponding OBS path, for example, **obs://hivetest/user/hive/warehouse/**.

      **vi** *Client installation directory*\ **/Hive/HCatalog/conf/hivemetastore-site.xml**

#. Go to the Hive Beeline CLI, create a database, and ensure that the location is an OBS path.

   **cd** *Client installation directory*

   **kinit** *Component operation user*

   **beeline**

   **create database testdb1;**

   **show create database testdb1;**

   |image2|

Configuring Ranger Permissions
------------------------------

-  Granting the read and write permissions on OBS paths to the **hive** user group

   #. Log in to the Ranger web UI as the Ranger administrator. On the home page, click component plug-in name **OBS** in the **EXTERNAL AUTHORIZATION** area, and assign the **Read** and **Write** permissions on the OBS storage path to the **hive** user group. If this operation is successful, all users in the **hive** group can access the Hive data warehouse path.

      For example, assign the **Read** and **Write** permissions on the **obs://hivetest/user/hive/warehouse/** directory to the **hive** user group:

      |image3|

   #. Choose **Settings** > **Roles**, click **Add New Role**, and create a role whose **Role Name** is **hive**.

      |image4|

-  Granting the read and write permissions on OBS paths to a custom user group

   #. Log in to FusionInsight Manager and choose **System** > **Permission** > **User Group**. On the displayed page, click **Create User Group**.

   #. Create a user group without a role, for example, **hiveobs1**, and bind the user group to the corresponding user.

   #. Log in to the Ranger management page as the **rangeradmin** user.

   #. On the home page, click component plug-in name **OBS** in the **EXTERNAL AUTHORIZATION** area.

   #. Grant the **Read** and **Write** permissions on the OBS storage path to the **hiveobs1** user group. In this case, all users bound to the **hiveobs1** user group can access the Hive data warehouse path.

      |image5|

-  Creating a database,table, or partition in a custom location and granting read and write permissions on OBS paths

   #. Log in to the Ranger web UI as the Ranger administrator.

   #. On the home page, click component plug-in name **OBS** in the **EXTERNAL AUTHORIZATION** area, and assign the **Read** and **Write** permissions on the OBS storage path to the user group of the corresponding user.

      For example, assign the **Read** and **Write** permissions on the **obs://obs-test/test/** directory to the **hgroup1** user group, as shown in the following figure.

      |image6|

   #. On the home page, click the component plug-in name **Hive** in the **HADOOP SQL** area, and add a URL policy that grants the **Read** and **Write** permissions on the OBS path to the user group of the corresponding user.

      For example, create the **hive_url_policy URL** policy for the **hgroup1** user group and assign the **Read** and **Write** permissions on the **obs://obs-test/test/** directory to the user group, as shown in the following figure.

      |image7|

   #. Log in to the beeline client and set **Location** to the OBS file system path when creating a table.

      **cd** *Client installation directory*

      **kinit** *Component operation user*

      **beeline**

      For example, to create a table named **test** whose **Location** is **obs://obs-test/test/**\ *Database name*\ **/**\ *Table name*, run the following command:

      **create external table test(name string) location "obs://obs-test/test/**\ *Database name*\ **/**\ *Table name*\ **";**

.. note::

   -  To authorize a view chart, you need to grant the view chart permission and the physical table path permission corresponding to the view chart.
   -  Cascading authorization can be performed only on databases and tables, and cannot be on partitions. If a partition path is not in the table path, you need to manually authorize the partition path.
   -  Cascading authorization for **Deny Conditions** in the Hive Ranger policy is not supported. That is, the Deny Conditions permission only restricts the table permission and cannot generate the permission of the HDFS/OBS storage source.
   -  The permission of the HDFS Ranger policy is prior to that of the HDFS/OBS storage source generated by cascading authorization. If the HDFS Ranger permission has been set for the HDFS storage source of the table, the cascading permission does not take effect.
   -  **alter** operations cannot be performed on tables whose storage source is OBS after cascading authorization. To perform the **alter** operation, you need to grant the **Read** and **Write** permissions of the parent directory of the OBS table path to the corresponding user group.

.. |image1| image:: /_static/images/en-us_image_0000001972894010.png
.. |image2| image:: /_static/images/en-us_image_0000002009454237.png
.. |image3| image:: /_static/images/en-us_image_0000002009573749.png
.. |image4| image:: /_static/images/en-us_image_0000001973053758.png
.. |image5| image:: /_static/images/en-us_image_0000001972894046.png
.. |image6| image:: /_static/images/en-us_image_0000002009454273.png
.. |image7| image:: /_static/images/en-us_image_0000002009573789.png
