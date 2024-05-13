:original_name: mrs_01_1286.html

.. _mrs_01_1286:

Interconnecting Hive with OBS
=============================

Before performing the following operations, ensure that you have configured a storage-compute decoupled cluster by referring to :ref:`Configuring a Storage-Compute Decoupled Cluster (Agency) <mrs_01_0768>` or :ref:`Configuring a Storage-Compute Decoupled Cluster (AK/SK) <mrs_01_0468>`.

When creating a table, set the table location to an OBS path.
-------------------------------------------------------------

#. Log in to the client installation node as the client installation user.

#. Run the following command to initialize environment variables:

   **source ${client_home}/bigdata_env**

#. For a security cluster, run the following command to perform user authentication (the user must have the permission to perform Hive operations). If Kerberos authentication is not enabled for the current cluster, you do not need to run this command.

   **kinit** *User performing Hive operations*

#. Log in to MRS Manager and choose **Cluster** > **Services** > **Hive** > **Configurations** > **All Configurations**.

   In the left navigation tree, choose **Hive** > **Customization**. In the customized configuration items, add **dfs.namenode.acls.enabled** to the **hdfs.site.customized.configs** parameter and set its value to **false**.

   |image1|

#. Click **Save**. Click the **Dashboard** tab and choose **More** > **Restart Service**. In the **Verify Identity** dialog box that is displayed, enter the password of the current user, and click **OK**. In the displayed **Restart Service** dialog box, select **Restart upper-layer services** and click **OK**. Hive is restarted.

#. Log in to the beeline client and set **Location** to the OBS file system path when creating a table.

   **beeline**

   For example, run the following command to create the table **test** in **obs://**\ *OBS parallel file system name*\ **/user/hive/warehouse/**\ *Database name*\ **/**\ *Table name*:

   **create table test(name string) location "obs://**\ *OBS parallel file system name*\ **/user/hive/warehouse/**\ *Database name*\ **/**\ *Table name*\ **";**

   .. note::

      You need to add the component operator to the URL policy in the Ranger policy. Set the URL to the complete path of the object on OBS. Select the Read and Write permissions.

Setting the Default Location of the Created Hive Table to the OBS Path
----------------------------------------------------------------------

#. Log in to MRS Manager and choose **Cluster** > **Services** > **Hive** > **Configurations** > **All Configurations**.

#. In the left navigation tree, choose **MetaStore** > **Customization**. Add **hive.metastore.warehouse.dir** to the **hive.metastore.customized.configs** parameter and set it to the OBS path.

#. In the left navigation tree, choose **HiveServer** > **Customization**. Add **hive.metastore.warehouse.dir** to the **hive.metastore.customized.configs** and **hive.metastore.customized.configs** parameters, and set it to the OBS path.

#. Save the configurations and restart Hive.

#. Update the client configuration file.

   a. Run the following command to open **hivemetastore-site.xml** in the Hive configuration file directory on the client:

      **vim /opt/Bigdata/client/Hive/config/hivemetastore-site.xml**

   b. Change the value of **hive.metastore.warehouse.dir** to the corresponding OBS path.

      |image2|

#. Log in to the beeline client, create a table, and check whether the location is the OBS path.

   **beeline**

   **create table test(name string);**

   **desc formatted test;**

   .. note::

      If the database location points to HDFS, the table to be created in the database (without specifying the location) also points to HDFS. If you want to modify the default table creation policy, change the location of the database to OBS by performing the following operations:

      a. Run the following command to query the location of the database:

         **show create database** *obs_test*\ **;**

         |image3|

      b. Run the following command to change the database location:

         **alter database** *obs_test* **set location** *'*\ **obs://**\ *OBS parallel file system name*\ **/user/hive/warehouse/**\ *Database name*\ **'**

         Run the **show create database** *obs_test* command to check whether the database location points to OBS.

         |image4|

      c. Run the following command to change the table location:

         **alter table** *user_info* **set location** *'*\ **obs://**\ *OBS parallel file system name*\ **/user/hive/warehouse/**\ *Database name*\ **/**\ *Table name*\ **'**

         If the table contains data, migrate the original data file to the new location.

.. |image1| image:: /_static/images/en-us_image_0000001440974397.png
.. |image2| image:: /_static/images/en-us_image_0000001295738104.png
.. |image3| image:: /_static/images/en-us_image_0000001348737917.png
.. |image4| image:: /_static/images/en-us_image_0000001296217540.png
