:original_name: alm_12042.html

.. _alm_12042:

ALM-12042 Key File Configurations Are Abnormal
==============================================

Description
-----------

The system checks key file configurations every hour. This alarm is generated if any key configuration is abnormal.

This alarm is cleared after the configuration becomes normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12042    Major          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
PathName    Specifies the file path or file name.
=========== =======================================================

Impact on the System
--------------------

Functions related to the file are abnormal.

Possible Causes
---------------

The user has manually modified the file configurations or the system has experienced an unexpected power-off.

Procedure
---------

#. Check the file configurations.

   a. Go to the MRS cluster details page and choose **Alarms**.
   b. In the details of the alarm, query the **HostName** (name of the alarmed host) and **PathName** (path or name of the involved file).
   c. Log in to the alarmed node.
   d. Manually check and modify the file configurations according to the criteria in :ref:`Related Information <alm_12042__en-us_topic_0191813944_section24734811164818>`.
   e. Wait until the next system check is complete and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12042__en-us_topic_0191813944_li572522141314>`.

#. .. _alm_12042__en-us_topic_0191813944_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

.. _alm_12042__en-us_topic_0191813944_section24734811164818:

Related Information
-------------------

-  **Checking** **/etc/fstab**

   Check whether partitions configured in **/etc/fstab** exist in **/proc/mounts** and whether swap partitions configured in **/etc/fstab** match those in **/proc/swaps**.

-  **Checking** **/etc/hosts**

   Run the **cat /etc/hosts** command. If any of the following situations exists, the file configurations are abnormal.

   -  The **/etc/hosts** file does not exist.
   -  The host name is not configured in the file.
   -  The IP address of the host is duplicate.
   -  The IP address of the host does not exist in the **ipconfig** list.
   -  An IP address in the file is used by multiple hosts.
