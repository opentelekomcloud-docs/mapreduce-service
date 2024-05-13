:original_name: admin_guide_000154.html

.. _admin_guide_000154:

Configuring SNMP Northbound Parameters
======================================

Scenario
--------

If users need to view alarms and monitoring data of a cluster on the O&M platform, you can use Simple Network Management Protocol (SNMP) on MRS Manager to report related data to the network management system (NMS).

Procedure
---------

#. Log in to MRS Manager.

#. Choose **System** > **Interconnection** > **SNMP**.

#. Toggle on **SNMP Service**.

   The SNMP service is disabled by default. |image1| indicates that the service is enabled.

#. Set interconnection parameters according to :ref:`Table 1 <admin_guide_000154__en-us_topic_0046736864_tab01>`.

   .. _admin_guide_000154__en-us_topic_0046736864_tab01:

   .. table:: **Table 1** Interconnection parameters

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                    |
      +===================================+================================================================================================================================+
      | Version                           | Specifies the version of SNMP, which can be:                                                                                   |
      |                                   |                                                                                                                                |
      |                                   | -  **V2C**: This is an earlier version with low security.                                                                      |
      |                                   | -  **V3**: This is a later version with higher security than SNMP V2C.                                                         |
      |                                   |                                                                                                                                |
      |                                   | SNMP V3 is recommended.                                                                                                        |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Local Port                        | Specifies the local port. The default value is **20000**. The value ranges from **1025** to **65535**.                         |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Read Community Name               | Specifies the read-only community name. This parameter is available only when **Version** is set to **V2C**.                   |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Write Community Name              | Specifies the write community name. This parameter is available only when **Version** is set to **V2C**.                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Security Username                 | Specifies the SNMP security username. This parameter is available only when **Version** is set to **V3**.                      |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Authentication Protocol           | Specifies the authentication protocol. This parameter is available only when **Version** is set to **V3**. SHA is recommended. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Authentication Password           | Specifies the authentication password. This parameter is available only when **Version** is set to **V3**.                     |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Confirm Password                  | Used to confirm the authentication password. This parameter is available only when **Version** is set to **V3**.               |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Encryption Protocol               | Specifies the encryption protocol. This parameter is available only when **Version** is set to **V3**. AES256 is recommended.  |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Encryption Password               | Specifies the encryption password. This parameter is available only when **Version** is set to **V3**.                         |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
      | Confirm Password                  | Used to confirm the encryption password. This parameter is available only when **Version** is set to **V3**.                   |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      -  The value of **Security Username** cannot contain repeated strings with the unit length as a common factor of 64 (such as 1, 2, 4, and 8), for example, **abab** and **abcdabcd**.
      -  The **Authentication Password** and **Encryption Password** must contain 8 to 16 characters, including at least three types of the following characters: uppercase letters, lowercase letters, digits, and special characters. The two passwords must be different. The two passwords cannot be the same as the security username or the reverse of the security username.
      -  For security purposes, periodically change the authentication password and encryption password when the SNMP protocol is used.
      -  If SNMP v3 is used, a security user will be locked after five consecutive authentication failures within 5 minutes. The user will be automatically unlocked 5 minutes later.

#. Click **Create Trap Target** in the **Trap Target** area. In the displayed dialog box, set the following parameters:

   -  **Target Symbol**: specifies the trap target ID, which is the ID of the NMS or host that receives traps. The value consists of 1 to 255 characters, including letters or digits.
   -  **Target IP Address Mode**: specifies the mode of the target IP address. The value can be **IPv4** or **IPv6**.
   -  **Target IP Address**: specifies the target IP address, which can communicate with the management plane IP address of the management node.
   -  **Target Port**: specifies the port receiving traps. The port number must be consistent with the peer end and ranges from 0 to 65535.
   -  **Trap Community Name**: This parameter is available only when **Version** is set to **V2C** and is used to report the community name.

   Click **OK**.

   The **Create Trap Target** dialog box is closed.

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001392414386.png
