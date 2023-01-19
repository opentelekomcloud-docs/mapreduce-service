:original_name: mrs_01_1762.html

.. _mrs_01_1762:

Why Cannot I Connect to HiveServer When I Use IBM JDK to Access the Beeline Client?
===================================================================================

Scenario
--------

When users check the JDK version used by the client, if the JDK version is IBM JDK, the Beeline client needs to be reconstructed. Otherwise, the client will fail to connect to HiveServer.

Procedure
---------

#. Log in to FusionInsight Manager and choose **System** > **Permission** > **User**. In the **Operation** column of the target user, choose **More** > **Download Authentication Credential**, select the cluster information, and click **OK** to download the keytab file.

#. Decompress the keytab file and use WinSCP to upload the decompressed **user.keytab** file to the Hive client installation directory on the node to be operated, for example, **/opt/client**.

#. Run the following command to open the **Hive/component_env** configuration file in the Hive client directory:

   **vi** *Hive client installation directory*\ **/Hive/component_env**

   Add the following content to the end of the line where **export CLIENT_HIVE_URI** is located:

   .. code-block::

      \; user.principal=Username @HADOOP.COM\;user.keytab=user.keytab file path/user.keytab
