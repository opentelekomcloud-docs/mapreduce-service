:original_name: mrs_01_0240.html

.. _mrs_01_0240:

Configuring SNMP Northbound Interface Parameters
================================================

Scenario
--------

You can configure the northbound interface so that alarms and monitoring metrics on MRS Manager can be integrated to the network management platform using SNMP.

Prerequisites
-------------

The ECS corresponding to the server must be in the same VPC as the Master node of the MRS cluster, and the Master node can access the IP address and specified port of the server.

Procedure
---------

#. On MRS Manager, click **System**.

#. In **Configuration**, click **Configure SNMP** under **Monitoring and Alarm**.

   The **SNMP Service** is disabled by default. Click the switch to enable the SNMP service.

#. Set the interconnection parameters listed in :ref:`Table 1 <mrs_01_0240__en-us_topic_0035209607_table981749184027>`.

   .. _mrs_01_0240__en-us_topic_0035209607_table981749184027:

   .. table:: **Table 1** Syslog parameters

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                    |
      +===================================+================================================================================================================================================================================+
      | Version                           | Specifies the version of the SNMP, which can be:                                                                                                                               |
      |                                   |                                                                                                                                                                                |
      |                                   | -  v2c: an earlier version with low security                                                                                                                                   |
      |                                   | -  v3: the latest version of SNMP with higher security than SNMPv2c                                                                                                            |
      |                                   |                                                                                                                                                                                |
      |                                   | The SNMP v3 version is recommended.                                                                                                                                            |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Local Port                        | Specifies the local port. The default value is **20000**. The value ranges from **1025** to **65535**.                                                                         |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Read Community Name               | Specifies the read-only community name. This parameter is valid only when **Version** is set to **v2c**.                                                                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Write Community Name              | Specifies the write community name. This parameter is valid only when **Version** is set to **v2c**.                                                                           |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Security Username                 | Specifies the SNMP security username. This parameter is valid only when **Version** is set to **v3**.                                                                          |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Authentication Protocol           | Specifies the authentication protocol. You are advised to set this parameter to set this parameter to **SHA**. This parameter is valid only when **Version** is set to **v3**. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Authentication Password           | Specifies the authentication key. This parameter is valid only when **Version** is set to **v3**.                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Confirm Password                  | Used to confirm the authentication key. This parameter is valid only when **Version** is set to **v3**.                                                                        |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Encryption Protocol               | Specifies the encryption protocol. You are advised to set this parameter to **AES256**. This parameter is valid only when **Version** is set to **v3**.                        |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Encryption Password               | Specifies the encryption key. This parameter is valid only when **Version** is set to **v3**.                                                                                  |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Confirm Password                  | Used to confirm the encryption key. This parameter is valid only when **Version** is set to **v3**.                                                                            |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      -  The **Authentication Password** and **Encryption Password** must contain 8 to 16 characters, including at least three types of the following characters: uppercase letters, lowercase letters, digits, and special characters. The two passwords must be different. The two passwords cannot be the same as the security username or the reverse of the security username.
      -  For security purposes, periodically change the authentication password and encryption password when the SNMP protocol is used.
      -  If SNMPv3 is used, a security user will be locked after five consecutive authentication failures within 5 minutes. The user will be automatically unlocked 5 minutes later.

#. Click **Create Trap Target** in the **Trap Target** area. In the displayed dialog box, set the following parameters:

   -  **Target Symbol** specifies the trap target ID, which is the ID of the NMS or host that receives traps. The value consists of 1 to 255 characters, including letters or digits.
   -  **Target IP Address** specifies the IP address of the target trap. IP addresses of class A, B, and C can be used to communicate with the IP address of the management plane of the management node.
   -  **Target Port** specifies the port receiving traps. The port number must be consistent with the peer end and ranges from 0 to 65535.
   -  **Trap Community Name** is valid only when **Version** is set to **v2c**.

   Click **OK**. The **Create Trap Target** dialog box is closed.

#. Click **OK** to complete the settings.
