:original_name: ALM-12042.html

.. _ALM-12042:

ALM-12042 Incorrect Configuration of Key Files
==============================================

Description
-----------

The system checks whether critical configurations are correct every 5 minutes. This alarm is generated when the configurations are abnormal.

This alarm is cleared when the configurations become normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12042    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service name for which the alarm is generated.      |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role name for which the alarm is generated.         |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the object (host ID) for which the alarm is generated.  |
+-------------+-------------------------------------------------------------------+
| PathName    | Specifies the path or name of the abnormal file.                  |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

Functions related to the file are abnormal.

Possible Causes
---------------

The file configuration is modified manually or the system is powered off unexpectedly.

Procedure
---------

**Check abnormal file configuration.**

#. On the MRS Manager portal, choose **O&M > Alarm > Alarms**.

#. Check the value of **HostName** to obtain the host name involved in this alarm. Check the value of **PathName** to obtain the path or name of the abnormal file.

#. Log in to the node for which the alarm is generated as user **root**.

#. View the $BIGDATA_LOG_HOME/nodeagent/scriptlog/checkfileconfig.log file and analyze the cause based on the error log. Locate the check standards of the file in the :ref:`Related Information <alm-12042__en-us_topic_0070543617_cab>` and manually check and modify the file based on the standards.

   Run the **vi** *file name* command to enter the editing mode, and then press **Insert** to start editing.

   After the modification is complete, press **Esc** to exit the editing mode and enter **:wq** to save the settings and exit.

   For example:

   **vi /etc/ssh/sshd_config**

#. Wait a hour and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12042__li1843685711310>`.

**Collect fault information.**

6. .. _alm-12042__li1843685711310:

   On the MRS Manager portal, choose **O&M** > **Log > Download**.

7. Select **NodeAgent** from the **Service** and click **OK**.

8. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

.. _alm-12042__en-us_topic_0070543617_cab:

Related Information
-------------------

-  **Check standards of /etc/fstab**

   Check whether the partitions configured in the **/etc/fstab** file can be found in **/proc/mounts**.

   Check whether the swap partitions configured in fstab correspond to those in /proc/swaps.

-  **Check the /etc/hosts configuration file.**

   Run **cat /ect/hosts**. If any of the following situations occurs, the **/etc/hosts** configuration file is abnormal:

   #. The **/etc/hosts** file does not exist.
   #. The host name is not configured in the file.
   #. The host name maps to multiple IP addresses in the file.
   #. The IP address corresponding to the host name does not exist in the command output of the **ifconfig** command.
   #. One IP address maps to multiple host names in the file.

-  **Check standards of /etc/ssh/sshd_config**

   Run the **vi /etc/ssh/sshd_config** command to check whether configuration items are configured as follows:

   #. The value of **UseDNS** must be set to **no**.
   #. The value of **MaxStartups** must be greater than or equal to 1000.
   #. At least one of the **PasswordAuthentication** and **ChallengeResponseAuthentication** parameters must be left blank or at least one of the parameters be set to **yes**.

.. |image1| image:: /_static/images/en-us_image_0000001532927502.png
