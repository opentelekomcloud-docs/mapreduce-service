:original_name: mrs_01_0572.html

.. _mrs_01_0572:

Updating Cluster Keys
=====================

Scenario
--------

When a cluster is installed, an encryption key is generated automatically to store the security information in the cluster (such as all database user passwords and key file access passwords) in encryption mode. After the cluster is successfully installed, you are advised to periodically update the encryption key based on the following procedure.

Impact on the System
--------------------

-  After a cluster key is updated, a new key is generated randomly in the cluster. This key is used to encrypt and decrypt the newly stored data. The old key is not deleted, and it is used to decrypt data encrypted using the old key. After security information is modified, for example, a database user password is changed, the new password is encrypted using the new key.
-  When the key is updated, the cluster is stopped and cannot be accessed.

Prerequisites
-------------

The upper-layer applications depending on the cluster are stopped.

Procedure
---------

#. Log in to MRS Manager and choose **Services** > **More** > **Stop Cluster**.

   In the displayed dialog box, select **I have read the information and understand the impact.** Click **OK**. Wait until the system displays a message indicating that the operation is successful. Click **Finish**. The cluster is stopped successfully.

#. Log in to the active management node.

#. Run the following commands to switch the user:

   **sudo su - omm**

#. Run the following command to disable logout upon timeout:

   **TMOUT=0**

#. Run the following command to switch the directory:

   **cd ${BIGDATA_HOME}/om-0.0.1/tools**

#. Run the following command to update the cluster key:

   **sh updateRootKey.sh**

   Enter **y** as prompted.

   .. code-block::

      The root key update is a critical operation.
      Do you want to continue?(y/n):

   The key is updated successfully if the following information is displayed:

   .. code-block::

      ...
      Step 4-1: The key save path is obtained successfully.
      ...
      Step 4-4: The root key is sent successfully.

#. On MRS Manager, choose **Services > More > Start Cluster**.

   In the displayed dialog box, click **OK**. After **Operation successful** is displayed, click **Finish**. The cluster is started.
