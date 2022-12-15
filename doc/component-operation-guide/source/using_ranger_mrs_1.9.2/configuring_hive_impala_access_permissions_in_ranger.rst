:original_name: mrs_01_0765.html

.. _mrs_01_0765:

Configuring Hive/Impala Access Permissions in Ranger
====================================================

After an MRS cluster with Ranger installed is created, Hive and Impala access control is not integrated into Ranger. This section describes how to integrate Hive into Ranger. Impala follows the same procedure.

#. Log in to the Ranger web UI.

#. In the **Service Manager** area, click |image1| next to **HIVE** to add a Hive service.


   .. figure:: /_static/images/en-us_image_0000001388415558.png
      :alt: **Figure 1** Adding a Hive service

      **Figure 1** Adding a Hive service

#. Set the parameters for adding a Hive service according to :ref:`Table 1 <mrs_01_0765__table54444329411>`. Use the default values for the parameters that are not listed in the table.

   .. _mrs_01_0765__table54444329411:

   .. table:: **Table 1** **Parameter description**

      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Description                                                                                                                                                                                                         | Example Value                                                                                                                  |
      +=======================+=====================================================================================================================================================================================================================+================================================================================================================================+
      | Service Name          | Name of the service to be created. The value is fixed to **hivedev**.                                                                                                                                               | hivedev                                                                                                                        |
      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Username              | You can set this parameter to any value.                                                                                                                                                                            | admin                                                                                                                          |
      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Password              | You can set this parameter to any value.                                                                                                                                                                            | ``-``                                                                                                                          |
      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | jdbc.driverClassName  | Driver class for connecting to Hive. The value is fixed to **org.apache.hive.jdbc.HiveDriver**.                                                                                                                     | org.apache.hive.jdbc.HiveDriver                                                                                                |
      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | jdbc.url              | URL for connecting to Hive. The format is ZooKeeper mode:                                                                                                                                                           | jdbc:hive2://xx.xx.xx.xx:2181,xx.xx.xx.xx:2181,xx.xx.xx.xx:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2 |
      |                       |                                                                                                                                                                                                                     |                                                                                                                                |
      |                       | jdbc:hive2://<host>:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2                                                                                                                             |                                                                                                                                |
      |                       |                                                                                                                                                                                                                     |                                                                                                                                |
      |                       | **<host>** indicates a ZooKeeper address. To obtain the ZooKeeper address, log in to MRS Manager, choose **Services** > **ZooKeeper** > **Instance**, and view the management IP address of the ZooKeeper instance. |                                                                                                                                |
      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+


   .. figure:: /_static/images/en-us_image_0000001349170337.png
      :alt: **Figure 2** Creating hivedev

      **Figure 2** Creating hivedev

#. Click **Add** to add the service.

#. Start the Ranger Hive plugin to authorize Ranger to manage Hive.

   a. On the MRS management console, click the cluster name to go to the cluster details page.
   b. Click the **Components** tab.
   c. Choose **Hive** > **Service Configuration** and switch **Basic** to **All**.
   d. Search for **hive.security.authorization** and modify the following configurations:

      -  hive.security.authorization.enabled = true
      -  hive.security.authorization.manager = org.apache.ranger.authorization.hive.authorizer.RangerHiveAuthorizerFactory

   e. Click **Save Configuration** and select **Restart the affected services or instances** to restart the Hive service.

#. Add an access control policy.

   a. Log in to the Ranger web UI.

   b. In the **HIVE** area, click the added service **hivedev**.

   c. Click **Add New Policy** to add an access control policy.

   d. Set the parameters according to :ref:`Table 2 <mrs_01_0765__table116322231534>`. Use the default values for the parameters that are not listed in the table.

      .. _mrs_01_0765__table116322231534:

      .. table:: **Table 2** Parameter description

         +-----------------------+-----------------------------------------------------------------------------------------+-------------------------------------------+
         | Parameter             | Description                                                                             | Example Value                             |
         +=======================+=========================================================================================+===========================================+
         | Policy Name           | Policy name                                                                             | Policy001                                 |
         +-----------------------+-----------------------------------------------------------------------------------------+-------------------------------------------+
         | database              | Name of the database that the policy allows to access                                   | test                                      |
         +-----------------------+-----------------------------------------------------------------------------------------+-------------------------------------------+
         | table                 | Name of the table corresponding to the database that the policy allows to access        | table1                                    |
         +-----------------------+-----------------------------------------------------------------------------------------+-------------------------------------------+
         | Hive Column           | Column name of the table corresponding to the database that the policy allows to access | name                                      |
         +-----------------------+-----------------------------------------------------------------------------------------+-------------------------------------------+
         | Allow Conditions      | -  **Select Group**: user group that the policy allows to access                        | -  Select Group: **testuser**             |
         |                       | -  **Select User**: user in the user group that the policy allows to access             | -  Select User: **testuser**              |
         |                       | -  **Permissions**: permissions that the policy allows the user to have                 | -  Permissions: **Create** and **Select** |
         +-----------------------+-----------------------------------------------------------------------------------------+-------------------------------------------+


      .. figure:: /_static/images/en-us_image_0000001348770629.png
         :alt: **Figure 3** Adding an access control policy for **hivedev**

         **Figure 3** Adding an access control policy for **hivedev**

   e. Click **Add** to add the policy. According to the preceding policy, user **testuser** in the **testuser** user group has the **Create** and **Select** permissions on the **name** column of **table1** in the **test** database of Hive, but no permissions to access other columns.

#. Log in to the Hive client by referring to :ref:`Using Hive from Scratch <mrs_01_0442>`, and check whether Hive has been integrated into Ranger.

   a. Run the following command to access the Hive beeline:

      **source /opt/client/bigdata_env**

      **beeline**

   b. Run the following command to set up a connection and log in as user **testuser**:

      **!connect jdbc:hive2://xx.xx.xx.xx:2181,xx.xx.3.81:2181,192.168.3.153:2181/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=hiveserver2**


      .. figure:: /_static/images/en-us_image_0000001438393405.png
         :alt: **Figure 4** Logging in to Hive

         **Figure 4** Logging in to Hive

   c. Query data and check whether Ranger is integrated.


      .. figure:: /_static/images/en-us_image_0000001349289921.png
         :alt: **Figure 5** Verifying the integration of Ranger with Hive

         **Figure 5** Verifying the integration of Ranger with Hive

.. |image1| image:: /_static/images/en-us_image_0000001296090600.png
