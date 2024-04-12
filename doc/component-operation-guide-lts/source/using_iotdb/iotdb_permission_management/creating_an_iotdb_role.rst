:original_name: mrs_01_24142.html

.. _mrs_01_24142:

Creating an IoTDB Role
======================

Create and configure an IoTDB role on Manager as an MRS cluster administrator. An IoTDB role can be configured with IoTDB administrator permissions or a common user's permissions to read, write, or delete data.

Prerequisites
-------------

-  The MRS cluster administrator has understood service requirements.
-  You have installed the IoTDB client.

Procedure
---------

#. On Manager, choose **System** > **Permission** > **Role**.

#. On the displayed page, click **Create Role** and specify **Role Name** and **Description**.

#. Configure **Configure Resource Permission**. For details, see :ref:`Table 1 <mrs_01_24142__t873a9c44357b40cd98cb948ce9438d93>`.

   IoTDB permissions:

   -  **Common User Privileges**: includes data operation permissions. Permissions on the IoTDB **root** directory, storage group, and any node path from a storage group to a time series can be granted selectively. The minimum permissions are read, write, modify, and delete permissions on the time series.
   -  **IoTDB Admin Privilege**: includes all permissions in :ref:`Table 1 <mrs_01_24141__table1392557124016>`.

   .. _mrs_01_24142__t873a9c44357b40cd98cb948ce9438d93:

   .. table:: **Table 1** Configuring a role

      +----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Scenario                                                             | Role Authorization                                                                                                                                                                                                                        |
      +======================================================================+===========================================================================================================================================================================================================================================+
      | Configuring the IoTDB administrator permission                       | In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **IoTDB** and select **IoTDB Admin Privilege**.                                                                                                    |
      +----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configuring the permission for users to create storage groups        | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **IoTDB** > **Common User Privileges**.                                                                                                         |
      |                                                                      | b. Select **Set StorageGroup** for the **root** directory.                                                                                                                                                                                |
      |                                                                      | c. A user with this permission can create storage groups in the **root** directory.                                                                                                                                                       |
      +----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configuring the permission for users to create time series           | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **IoTDB** > **Common User Privileges**.                                                                                                         |
      |                                                                      | b. Select **Create** for the **root** directory. You will have the permission to create time series in all recursive paths in the **root** directory.                                                                                     |
      |                                                                      | c. Click **root** to go to the storage group page and select the **Create** permission for the corresponding storage group. You will have the permission to create time series in all recursive paths in the storage group directory.     |
      +----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configuring the permission for users to modify time series           | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **IoTDB** > **Common User Privileges**.                                                                                                         |
      |                                                                      | b. Select **Alter** for the **root** directory. You will have the permission to modify time series in all recursive paths in the **root** directory.                                                                                      |
      |                                                                      | c. Click **root** to go to the storage group page and select the **Alter** permission for the corresponding storage group. You will have the permission to modify time series in all recursive paths of the storage group.                |
      |                                                                      | d. Click the specified storage group to go the time series page and select the **Alter** permission for the corresponding time series. You will have the permission to modify the time series.                                            |
      +----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configuring the permission for users to insert data into time series | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **IoTDB** > **Common User Privileges**.                                                                                                         |
      |                                                                      | b. Select **Insert** for the **root** directory. You will have the permission to insert data into the time series in all recursive paths in the **root** directory.                                                                       |
      |                                                                      | c. Click **root** to go to the storage group page and select the **Insert** permission for the corresponding storage group. You will have the permission to insert data into the time series in all recursive paths of the storage group. |
      |                                                                      | d. Click the specified storage group to go the time series page and select the **Insert** permission for the corresponding time series. You will have the permission to insert data into the time series.                                 |
      +----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configuring the permission for users to read data from time series   | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **IoTDB** > **Common User Privileges**.                                                                                                         |
      |                                                                      | b. Select **Read** for the **root** directory. You will have the permission to read data from the time series in all recursive paths in the **root** directory.                                                                           |
      |                                                                      | c. Click **root** to go to the storage group page and select the **Read** permission for the corresponding storage group. You will have the permission to read data from the time series in all recursive paths of the storage group.     |
      |                                                                      | d. Click the specified storage group to go the time series page and select the **Read** permission for the corresponding time series. You will have the permission to read data from the time series.                                     |
      +----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configuring the permission for users to delete time series           | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **IoTDB** > **Common User Privileges**.                                                                                                         |
      |                                                                      | b. Select **Delete** for the **root** directory. You will have the permission to delete data or time series in all recursive paths in the **root** directory.                                                                             |
      |                                                                      | c. Click **root** to go to the storage group page and select the **Delete** permission for the corresponding storage group. You will have the permission to delete data or time series in all recursive paths of the storage group.       |
      |                                                                      | d. Click the specified storage group to go the time series page and select the **Delete** permission for the corresponding time series. You will have the permission to delete data from the time series or delete the time series.       |
      +----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
