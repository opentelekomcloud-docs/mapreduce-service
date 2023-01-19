:original_name: mrs_01_24022.html

.. _mrs_01_24022:

Creating a Data Connection on the Flink Web UI
==============================================

Scenario
--------

Different data services can be accessed through data connections. Currently, FlinkServer supports HDFS, Kafka data connections.

Creating a Data Connection
--------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.

#. Choose **System Management** > **Data Connection Management**. The **Data Connection Management** page is displayed.

#. Click **Create Data Connection**. On the displayed page, select a data connection type, enter information by referring to :ref:`Table 1 <mrs_01_24022__en-us_topic_0000001219230571_table134890201518>`, and click **OK**.

   .. _mrs_01_24022__en-us_topic_0000001219230571_table134890201518:

   .. table:: **Table 1** Parameters for creating a data connection

      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
      | Parameter             | Description                                                                                                                                                 | Example Value                       |
      +=======================+=============================================================================================================================================================+=====================================+
      | Data Connection Type  | Type of the data connection, which can be **HDFS**, **Kafka**.                                                                                              | ``-``                               |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
      | Data Connection Name  | Name of the data connection, which can contain a maximum of 100 characters. Only letters, digits, and underscores (_) are allowed.                          | ``-``                               |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
      | Cluster Connection    | Cluster connection name in configuration management.                                                                                                        | ``-``                               |
      |                       |                                                                                                                                                             |                                     |
      |                       | This parameter is mandatory for HDFS data connections.                                                                                                      |                                     |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
      | Kafka broker          | Connection information about Kafka broker instances. The format is *IP address*:*Port number*. Use commas (,) to separate multiple instances.               | 192.168.0.1:21005,192.168.0.2:21005 |
      |                       |                                                                                                                                                             |                                     |
      |                       | This parameter is mandatory for Kafka data connections.                                                                                                     |                                     |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
      | Authentication Mode   | -  **SIMPLE**: indicates that the connected service is in non-security mode and does not need to be authenticated.                                          | ``-``                               |
      |                       | -  **KERBEROS**: indicates that the connected service is in security mode and the Kerberos protocol for security authentication is used for authentication. |                                     |
      |                       |                                                                                                                                                             |                                     |
      |                       | This parameter is mandatory for Kafka data connections.                                                                                                     |                                     |
      +-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+

Editing a Data Connection
-------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Choose **System Management** > **Data Connection Management**. The **Data Connection Management** page is displayed.
#. In the **Operation** column of the item to be modified, click **Edit**. On the displayed page, modify the connection information by referring to :ref:`Table 1 <mrs_01_24022__en-us_topic_0000001219230571_table134890201518>` and click **OK**.

Testing a Data Connection
-------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Choose **System Management** > **Data Connection Management**. The **Data Connection Management** page is displayed.
#. In the **Operation** column of the item to be tested, click **Test**.

Searching for a Data Connection
-------------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Choose **System Management** > **Data Connection Management**. The **Data Connection Management** page is displayed.
#. In the upper right corner of the page, you can search for a data connection by name.

Deleting a Data Connection
--------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Choose **System Management** > **Data Connection Management**. The **Data Connection Management** page is displayed.
#. In the **Operation** column of the item to be deleted, click **Delete**, and click **OK** in the displayed page.
