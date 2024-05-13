:original_name: mrs_01_24051.html

.. _mrs_01_24051:

Configuring Ranger Data Connections
===================================

Switch the Ranger metadata of the existing cluster to the metadata stored in the RDS database. This operation enables multiple MRS clusters to share the same metadata, and the metadata will not be deleted when the clusters are deleted. In this way, Ranger metadata migration is not required during cluster migration.

Prerequisites
-------------

You have created an RDS MySQL database instance. For details, see :ref:`Creating a Data Connection <mrs_01_0633__section813712431913>`.

.. note::

   -  For versions earlier than MRS 3.x, if the selected data connection is an **RDS MySQL database**, ensure that the database user is a **root** user. If the user is not **root**, create a user and grant permissions to the user by referring to :ref:`Performing Operations Before Data Connection <mrs_01_0633__section311713549458>`.
   -  In MRS 3.x or later, if the selected data connection is **RDS MySQL database**, the database user cannot be user **root**. In this case, create a user and grant permissions to the user by following the instructions provided in :ref:`Performing Operations Before Data Connection <mrs_01_0633__section311713549458>`.

Preparing for MySQL Database Ranger Metadata Configuration
----------------------------------------------------------

This operation is required only for **MRS 3.1.0 or later**.

#. Log in to MRS Manager. For details, see :ref:`Accessing MRS Manager <mrs_01_0129>`. Choose **Clusters** > **Services** > *Service name*.

   Currently, the following components in an MRS 3.1.\ *x* cluster support Ranger authentication: HDFS, HBase, Hive, Spark, Impala, Storm, and Kafka.

#. In the upper right corner of the **Dashboard** page, click **More** and select **Disable Ranger**. If **Disable Ranger** is dimmed, Ranger authentication is disabled, as shown in :ref:`Figure 1 <mrs_01_24051__fig14437127109>`.

   .. _mrs_01_24051__fig14437127109:

   .. figure:: /_static/images/en-us_image_0000001296217820.png
      :alt: **Figure 1** Disabling Ranger authentication

      **Figure 1** Disabling Ranger authentication

#. (Optional) To use an existing authentication policy, perform this step to export the authentication policy on the Ranger web page. After the Ranger metadata is switched, you can import the existing authentication policy again. The following uses Hive as an example. After the export, a policy file in JSON format is generated in a local directory.

   a. Log in to MRS Manager.

   b. Choose **Cluster** > **Services** > **Ranger** to go to the Ranger service overview page.

   c. Click **RangerAdmin** in the **Basic Information** area to go to the Ranger web UI.

      The **admin** user in Ranger belongs to the **User** type. To view all management pages, click the username in the upper right corner and select **Log Out** to log out of the system.

   d. Log in to the system as user **rangeradmin** (default password: **Rangeradmin@123**) or another user who has the Ranger administrator permissions.

   e. Click the export button |image1| in the row where the Hive component is located to export the authentication policy.


      .. figure:: /_static/images/en-us_image_0000001440726389.png
         :alt: **Figure 2** Exporting authentication policies

         **Figure 2** Exporting authentication policies

   f. .. _mrs_01_24051__li1947954718720:

      Click **Export**. After the export is complete, a policy file in JSON format is generated in a local directory.


      .. figure:: /_static/images/en-us_image_0000001348738221.png
         :alt: **Figure 3** Exporting Hive authentication policies

         **Figure 3** Exporting Hive authentication policies

Configuring a Data Connection for an MRS Cluster
------------------------------------------------

#. Log in to the MRS console.

#. Click the name of the cluster to view its details.

#. Click **Manage** on the right of **Data Connection** to go to the data connection configuration page.

#. Click **Configure Data Connection** and set related parameters.

   -  **Component Name**: Ranger
   -  **Module Type**: Ranger metadata
   -  **Connection Type**: RDS MySQL database
   -  **Connection Instance**: Select a created RDS MySQL DB instance. To create a new data connection, see :ref:`Creating a Data Connection <mrs_01_0633__section813712431913>`.

#. Select **I understand the consequences of performing the scale-in operation** and click **Test**.

#. After the test is successful, click **OK** to complete the data connection configuration.

#. Log in to MRS Manager.

#. Choose **Cluster** > **Services** > **Ranger** to go to the Ranger service overview page.

#. Choose **More** > **Restart Service** or **More** > **Service Rolling Restart**.

   If you choose **Restart Service**, services will be interrupted during the restart. If you select **Service Rolling Restart**, rolling restart can minimize the impact or do not affect service running.

   Restarting Ranger will affect the permissions of all components controlled by Ranger and may affect the normal running of services. Therefore, restart Ranger when the cluster is idle or during off-peak hours. Before the Ranger component is restarted, the policies in the Ranger component still take effect.


   .. figure:: /_static/images/en-us_image_0000001296058188.png
      :alt: **Figure 4** Restarting a service

      **Figure 4** Restarting a service

#. Enable Ranger authentication for the component to be authenticated. The Hive component is used as an example.

   Currently, the following components in an MRS 3.1.\ *x* cluster support Ranger authentication: HDFS, HBase, Hive, Spark, Impala, Storm, and Kafka.

   a. Log in to MRS Manager and choose **Cluster** > **Services** > *Service Name*.

   b. In the upper right corner of the **Dashboard** page, click **More** and select **Enable Ranger**.


      .. figure:: /_static/images/en-us_image_0000001295738404.png
         :alt: **Figure 5** Enabling Ranger authentication

         **Figure 5** Enabling Ranger authentication

#. Log in to the Ranger web UI and click the import button |image2| in the row of the Hive component.

   |image3|

#. Import parameters.

   -  Click **Select file** and select the authentication policy file downloaded in :ref:`3.f <mrs_01_24051__li1947954718720>`.
   -  Select **Merge If Exist Policy**.


   .. figure:: /_static/images/en-us_image_0000001296217824.png
      :alt: **Figure 6** Importing authentication policies

      **Figure 6** Importing authentication policies

#. Restart the component for which Ranger authentication is enabled.

   a. Log in to MRS Manager.

   b. Choose **Cluster** > **Services** > **Hive** to go to the Hive service overview page.

   c. Choose **More** > **Restart Service** or **More** > **Service Rolling Restart**.

      If you choose **Restart Service**, services will be interrupted during the restart. If you select **Service Rolling Restart**, rolling restart can minimize the impact or do not affect service running.

.. |image1| image:: /_static/images/en-us_image_0000001296217832.png
.. |image2| image:: /_static/images/en-us_image_0000001348738213.png
.. |image3| image:: /_static/images/en-us_image_0000001440367085.png
