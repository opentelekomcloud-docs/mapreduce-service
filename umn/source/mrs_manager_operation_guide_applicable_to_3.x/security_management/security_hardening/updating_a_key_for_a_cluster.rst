:original_name: admin_guide_000279.html

.. _admin_guide_000279:

Updating a Key for a Cluster
============================

Scenario
--------

When a cluster is installed, an encryption key is generated automatically by the system so that the security information in the cluster (such as all database user passwords and key file access passwords) can be stored in encryption mode. After the cluster is installed, if the original key is accidentally disclosed or a new key is required, you can manually update the key.

Impact on the System
--------------------

-  After a cluster key is updated, a new key is generated randomly in the cluster. This key is used to encrypt and decrypt the newly stored data. The old key is not deleted, and it is used to decrypt data encrypted using the old key. After security information is modified, for example, a database user password is changed, the new password is encrypted using the new key.
-  When a key is updated for a cluster, the cluster must be stopped and cannot be accessed.

Prerequisites
-------------

-  You have obtained the IP addresses of the active and standby management nodes. For details, see :ref:`Logging In to the Management Node <admin_guide_000005>`.
-  You have stopped the upper-layer service applications that depend on the cluster.

Procedure
---------

#. Log in to MRS Manager.

#. Choose **Cluster** > *Name of the desired cluster* and click **Stop**. In the dialog box that is displayed, enter the password of the current user

   and click **OK**. Wait for a while until a message indicating that the operation is successful is displayed.

#. Log in to the active management node as user **omm**.

#. Run the following command to disable logout upon timeout:

   **TMOUT=0**

   .. note::

      After the operations in this section are complete, run the **TMOUT=**\ *Timeout interval* command to restore the timeout interval in a timely manner. For example, **TMOUT=600** indicates that a user is logged out if the user does not perform any operation within 600 seconds.

#. Run the following command to go to the related directory:

   **cd ${BIGDATA_HOME}/om-server/om/tools**

#. Run the following command to update the cluster key:

   **sh updateRootKey.sh**

   Enter **y** as prompted.

   .. code-block::

      The root key update is a critical operation.
      Do you want to continue?(y/n):

   If the following information is displayed, the key is updated successfully.

   .. code-block::

      Step 4-1: The key save path is obtained successfully.
      ...
      Step 4-4: The root key is sent successfully.

#. On MRS Manager, click **Cluster**, click the name of the desired cluster, and click **Start**.

   In the displayed dialog box, click **OK**. Wait until a message is displayed, indicating that the startup is successful.
