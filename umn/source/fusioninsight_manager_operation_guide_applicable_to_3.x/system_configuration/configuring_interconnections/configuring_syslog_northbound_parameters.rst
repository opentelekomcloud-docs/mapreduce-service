:original_name: admin_guide_000155.html

.. _admin_guide_000155:

Configuring Syslog Northbound Parameters
========================================

Scenario
--------

If users need to view alarms and events of a cluster on the unified alarm reporting platform, you can use the Syslog protocol on FusionInsight Manager to report related data to the alarm platform.

.. important::

   If the Syslog protocol is not encrypted, data may be stolen.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **System** > **Interconnection** > **Syslog**.

#. Toggle on **Syslog Service**.

   The Syslog service is disabled by default. |image1| indicates that the service is enabled.

#. Set northbound parameters according to :ref:`Table 1 <admin_guide_000155__tba2589a9e61145faacec7d81c6eb3235>`.

   .. _admin_guide_000155__tba2589a9e61145faacec7d81c6eb3235:

   .. table:: **Table 1** Syslog interconnection parameters

      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter Area            | Parameter                          | Description                                                                                                                                                                                                                                                                                                     |
      +===========================+====================================+=================================================================================================================================================================================================================================================================================================================+
      | Syslog Protocol           | Server IP Address Mode             | Specifies the IP address mode of the interconnected server. The value can be **IPV4** or **IPV6**.                                                                                                                                                                                                              |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Server IP Address                  | Specifies the IP address of the interconnected server.                                                                                                                                                                                                                                                          |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Server Port                        | Specifies the port number for interconnection.                                                                                                                                                                                                                                                                  |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Protocol                           | Specifies the protocol type. The options are as follows:                                                                                                                                                                                                                                                        |
      |                           |                                    |                                                                                                                                                                                                                                                                                                                 |
      |                           |                                    | -  **TCP**                                                                                                                                                                                                                                                                                                      |
      |                           |                                    | -  **UDP**                                                                                                                                                                                                                                                                                                      |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Severity Level                     | Specifies the severity of the reported message. The options are as follows:                                                                                                                                                                                                                                     |
      |                           |                                    |                                                                                                                                                                                                                                                                                                                 |
      |                           |                                    | -  **Emergency**                                                                                                                                                                                                                                                                                                |
      |                           |                                    | -  **Alert**                                                                                                                                                                                                                                                                                                    |
      |                           |                                    | -  **Critical**                                                                                                                                                                                                                                                                                                 |
      |                           |                                    | -  **Error**                                                                                                                                                                                                                                                                                                    |
      |                           |                                    | -  **Warning**                                                                                                                                                                                                                                                                                                  |
      |                           |                                    | -  **Notice**                                                                                                                                                                                                                                                                                                   |
      |                           |                                    | -  **Informational** (default value)                                                                                                                                                                                                                                                                            |
      |                           |                                    | -  **Debug**                                                                                                                                                                                                                                                                                                    |
      |                           |                                    |                                                                                                                                                                                                                                                                                                                 |
      |                           |                                    |    .. note::                                                                                                                                                                                                                                                                                                    |
      |                           |                                    |                                                                                                                                                                                                                                                                                                                 |
      |                           |                                    |       **Severity Level** and **Facility** determine the priority of the sent message.                                                                                                                                                                                                                           |
      |                           |                                    |                                                                                                                                                                                                                                                                                                                 |
      |                           |                                    |       **Priority** = **Facility** x 8 + **Severity Level**                                                                                                                                                                                                                                                      |
      |                           |                                    |                                                                                                                                                                                                                                                                                                                 |
      |                           |                                    |       For details about the values of **Severity Level** and **Facility**, see :ref:`Table 2 <admin_guide_000155__t05bc8524f4804c44982ceceae14e8388>`.                                                                                                                                                          |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Facility                           | Specifies the module where the log is generated. For details about the available values of this parameter, see :ref:`Table 2 <admin_guide_000155__t05bc8524f4804c44982ceceae14e8388>`. Default value **local use 0 (local0)** is recommended.                                                                   |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Identifier                         | Specifies the product ID. The default value is **FusionInsight Manager**.                                                                                                                                                                                                                                       |
      |                           |                                    |                                                                                                                                                                                                                                                                                                                 |
      |                           |                                    | The identifier can contain a maximum of 256 characters, including letters, digits, underscores (_), periods (.), hyphens (-), spaces, and the following special characters: \| $ { }                                                                                                                            |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Report Message            | Report Format                      | Specifies the message format of the alarm report. For details, see the help information on the page.                                                                                                                                                                                                            |
      |                           |                                    |                                                                                                                                                                                                                                                                                                                 |
      |                           |                                    | The report format can contain a maximum of 1024 characters, including letters, digits, underscores (_), periods (.), hyphens (-), spaces, and the following special characters: \| $ { }                                                                                                                        |
      |                           |                                    |                                                                                                                                                                                                                                                                                                                 |
      |                           |                                    | .. note::                                                                                                                                                                                                                                                                                                       |
      |                           |                                    |                                                                                                                                                                                                                                                                                                                 |
      |                           |                                    |    For details about each field in the report format, see :ref:`Table 3 <admin_guide_000155__t614aa61f080f47f0ba68c57aa68e7dc1>`.                                                                                                                                                                               |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Alarm Type                         | Specifies the type of the alarm to be reported.                                                                                                                                                                                                                                                                 |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Alarm Severities                   | Specifies the level of the alarm to be reported.                                                                                                                                                                                                                                                                |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Uncleared Alarm Reporting | Periodic Uncleared Alarm Reporting | Specifies whether to report uncleared alarms in a specified period. You can toggle on or off the function. The function is toggled off by default.                                                                                                                                                              |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Report Interval (min)              | Specifies the interval for periodically reporting uncleared alarms. This parameter is valid only when **Periodic Uncleared Alarm Reporting** is enabled. The default value is **15**, in minutes. The value ranges from **5** to **1440** (one day).                                                            |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Heartbeat Settings        | Heartbeat Reporting                | Specifies whether to periodically report Syslog heartbeat messages. You can toggle on or off the function. The function is toggled off by default.                                                                                                                                                              |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Heartbeat Interval (minutes)       | Specifies the interval for periodically reporting heartbeat messages. This parameter is valid only when **Heartbeat Reporting** is enabled. The default value is **15**, in minutes. The value ranges from **1** to **60**.                                                                                     |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | Heartbeat Packet                   | Specifies the heartbeat message to be reported. This parameter is valid when **Heartbeat Reporting** is toggled on and cannot be left blank. The value can contain a maximum of 256 characters, including digits, letters, underscores (_), vertical bars (|), colons (:), spaces, commas (,), and periods (.). |
      +---------------------------+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      After the periodic heartbeat packet function is enabled, packets may be interrupted during automatic recovery of some cluster error tolerance (for example, active/standby OMS switchover). In this case, wait for automatic recovery.

#. Click **OK**.

Related Information
-------------------

.. _admin_guide_000155__t05bc8524f4804c44982ceceae14e8388:

.. table:: **Table 2** Numeric codes of **Severity Level** and **Facility**

   ============== ======================================== ============
   Severity Level Facility                                 Numeric Code
   ============== ======================================== ============
   **Emergency**  kernel messages                          0
   **Alert**      user-level messages                      1
   **Critical**   mail system                              2
   **Error**      system daemons                           3
   **Warning**    security/authorization messages (note 1) 4
   **Notice**     messages generated internally by syslog  5
   Informational  line printer subsystem                   6
   **Debug**      network news subsystem                   7
   ``-``          UUCP subsystem                           8
   ``-``          clock daemon (note 2)                    9
   ``-``          security/authorization messages (note 1) 10
   ``-``          FTP daemon                               11
   ``-``          NTP subsystem                            12
   ``-``          log audit (note 1)                       13
   ``-``          log alert (note 1)                       14
   ``-``          clock daemon (note 2)                    15
   ``-``          local use 0~7 (local0 ~ local7)          16 to 23
   ============== ======================================== ============

.. _admin_guide_000155__t614aa61f080f47f0ba68c57aa68e7dc1:

.. table:: **Table 3** Report format information fields

   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | Information Field                 | Description                                                                                |
   +===================================+============================================================================================+
   | dn                                | Cluster name                                                                               |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | id                                | Alarm ID                                                                                   |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | name                              | Alam name                                                                                  |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | serialNo                          | Alarm serial number                                                                        |
   |                                   |                                                                                            |
   |                                   | .. note::                                                                                  |
   |                                   |                                                                                            |
   |                                   |    The serial numbers of the fault alarms and the corresponding clear alarms are the same. |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | category                          | Alarm type. The options are as follows:                                                    |
   |                                   |                                                                                            |
   |                                   | -  **0**: fault alarm                                                                      |
   |                                   | -  **1**: clear alarm                                                                      |
   |                                   | -  **2**: event                                                                            |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | occurTime                         | Time when the alarm was generated                                                          |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | clearTime                         | Time when this alarm was cleared                                                           |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | isAutoClear                       | Whether an alarm is automatically cleared. The options are as follows:                     |
   |                                   |                                                                                            |
   |                                   | -  **1**: yes                                                                              |
   |                                   | -  **0**: no                                                                               |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | locationInfo                      | Location where the alarm was generated                                                     |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | clearType                         | Alarm clearance type. The options are as follows:                                          |
   |                                   |                                                                                            |
   |                                   | -  **-1**: not cleared                                                                     |
   |                                   | -  **0**: automatically cleared                                                            |
   |                                   | -  **2**: manually cleared                                                                 |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | level                             | Severity. The options are as follows:                                                      |
   |                                   |                                                                                            |
   |                                   | -  **1**: critical alarm                                                                   |
   |                                   | -  **2**: major alarm                                                                      |
   |                                   | -  **3**: minor alarm                                                                      |
   |                                   | -  **4**: warning alarm                                                                    |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | cause                             | Alarm cause                                                                                |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | additionalInfo                    | Additional information                                                                     |
   +-----------------------------------+--------------------------------------------------------------------------------------------+
   | object                            | Alarm object                                                                               |
   +-----------------------------------+--------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001392414386.png
