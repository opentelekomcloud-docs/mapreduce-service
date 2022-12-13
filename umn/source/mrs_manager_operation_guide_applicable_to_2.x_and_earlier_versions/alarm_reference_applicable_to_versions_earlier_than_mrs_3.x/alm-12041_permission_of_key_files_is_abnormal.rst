:original_name: alm_12041.html

.. _alm_12041:

ALM-12041 Permission of Key Files Is Abnormal
=============================================

Description
-----------

The system checks the permission, users, and user groups of key directories or files every hour. This alarm is generated if any of these is abnormal.

This alarm is cleared after the problem that causes abnormal permission, users, or user groups is solved.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12041    Major          Yes
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

System functions are unavailable.

Possible Causes
---------------

The user has manually modified the file permission, user information, or user groups, or the system has experienced an unexpected power-off.

Procedure
---------

#. Check the file permission.

   a. Go to the MRS cluster details page and choose **Alarms**.

   b. In the details of the alarm, query the **HostName** (name of the alarmed host) and **PathName** (path or name of the involved file).

   c. Log in to the alarmed node.

   d. Run the **ll** *PathName* command to query the current user, permission, and user group of the file or path.

   e. .. _alm_12041__en-us_topic_0191813951_li5250207310354:

      Go to the **${BIGDATA_HOME}/nodeagent/etc/agent/autocheck** directory and run the **vi keyfile** command. Search for the name of the involved file and query the correct permission of the file.

   f. Compare the actual permission of the file with the permission obtained in :ref:`1.e <alm_12041__en-us_topic_0191813951_li5250207310354>`. If they are different, change the actual permission, user information, and user group to the correct values.

   g. Wait until the next system check is complete and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12041__en-us_topic_0191813951_li572522141314>`.

#. .. _alm_12041__en-us_topic_0191813951_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
