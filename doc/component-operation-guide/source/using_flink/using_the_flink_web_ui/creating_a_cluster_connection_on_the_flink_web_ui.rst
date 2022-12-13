:original_name: mrs_01_24021.html

.. _mrs_01_24021:

Creating a Cluster Connection on the Flink Web UI
=================================================

Scenario
--------

Different clusters can be accessed by configuring the cluster connection.

Creating a Cluster Connection
-----------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.

#. Choose **System Management** > **Cluster Connection Management**. The **Cluster Connection Management** page is displayed.

#. Click **Create Cluster Connection**. On the displayed page, set parameters by referring to :ref:`Table 1 <mrs_01_24021__table134890201518>` and click **OK**.

   .. _mrs_01_24021__table134890201518:

   .. table:: **Table 1** Parameters for creating a cluster connection

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                |
      +===================================+============================================================================================================================================================================================+
      | Cluster Connection Name           | Name of the cluster connection, which can contain a maximum of 100 characters. Only letters, digits, and underscores (_) are allowed.                                                      |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                       | Description of the cluster connection name.                                                                                                                                                |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | FusionInsight HD Version          | Set a cluster version.                                                                                                                                                                     |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Secure Version                    | -  If the secure version is used, select **Yes** for a security cluster. Enter the username and upload the user credential.                                                                |
      |                                   | -  If not, select **No**.                                                                                                                                                                  |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Username                          | The user must have the minimum permissions for accessing services in the cluster. The name can contain a maximum of 100 characters. Only letters, digits, and underscores (_) are allowed. |
      |                                   |                                                                                                                                                                                            |
      |                                   | This parameter is available only when **Secure Version** is set to **Yes**.                                                                                                                |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Client Profile                    | Client profile of the cluster, in TAR format.                                                                                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | User Credential                   | User authentication credential in FusionInsight Manager in TAR format.                                                                                                                     |
      |                                   |                                                                                                                                                                                            |
      |                                   | This parameter is available only when **Secure Version** is set to **Yes**.                                                                                                                |
      |                                   |                                                                                                                                                                                            |
      |                                   | Files can be uploaded only after the username is entered.                                                                                                                                  |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      To obtain the cluster client configuration files, perform the following steps:

      a. Log in to FusionInsight Manager and choose **Cluster** > **Dashboard**.
      b. Choose **More** > **Download Client** > **Configuration Files Only**, select a platform type, and click **OK**.

      To obtain the user credential, perform the following steps:

      a. Log in to FusionInsight Manager and click **System**.
      b. In the **Operation** column of the user, choose **More** > **Download Authentication Credential**, select a cluster, and click **OK**.

Editing a Cluster Connection
----------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Choose **System Management** > **Cluster Connection Management**. The **Cluster Connection Management** page is displayed.
#. In the **Operation** column of the item to be modified, click **Edit**. On the displayed page, modify the connection information by referring to :ref:`Table 1 <mrs_01_24021__table134890201518>` and click **OK**.

Testing a Cluster Connection
----------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Choose **System Management** > **Cluster Connection Management**. The **Cluster Connection Management** page is displayed.
#. In the **Operation** column of the item to be tested, click **Test**.

Searching for a Cluster Connection
----------------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Choose **System Management** > **Cluster Connection Management**. The **Cluster Connection Management** page is displayed.
#. In the upper right corner of the page, you can enter a search criterion to search for and view the cluster connection based on **Cluster Connection Name**.

Deleting a Cluster Connection
-----------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Choose **System Management** > **Cluster Connection Management**. The **Cluster Connection Management** page is displayed.
#. In the **Operation** column of the item to be deleted, click **Delete**, and click **OK** in the displayed page.
