:original_name: mrs_03_1210.html

.. _mrs_03_1210:

How Do I Modify the allow_drop_detached Parameter of ClickHouse?
================================================================

#. Log in to the node where the ClickHouse client is located as user **root**.

#. Run the following commands to go to the client installation directory and set the environment variables:

   **cd /opt/**\ *Client installation directory*

   **source** **bigdata_env**

#. If Kerberos authentication is enabled for the cluster, run the following command to authenticate the user. If Kerberos authentication is disabled, skip this step.

   **kinit** *MRS cluster user*

   .. note::

      The user must have the ClickHouse administrator permissions.

#. Run the **clickhouse client --host** *192.168.42.90* **--secure -m** command, in which *192.168.42.90* indicates the IP address of the ClickHouseServer instance node. The command output is as follows:

   .. code-block:: console

      [root@server-2110082001-0017 hadoopclient]# clickhouse client --host 192.168.42.90 --secure -m
      ClickHouse client version 21.3.4.25.
      Connecting to 192.168.42.90:21427.
      Connected to ClickHouse server version 21.3.4 revision 54447.

#. Run the following command to set the value of the **allow_drop_detached** parameter, for example, **1**:

   **set allow_drop_detached=1;**

#. Run the following command to query the value of the **allow_drop_detached** parameter:

   **SELECT \* FROM system.settings WHERE name = 'allow_drop_detached';**

   |image1|

#. Run the **q;** command to exit the ClickHouse client.

.. |image1| image:: /_static/images/en-us_image_0000001223688037.png
