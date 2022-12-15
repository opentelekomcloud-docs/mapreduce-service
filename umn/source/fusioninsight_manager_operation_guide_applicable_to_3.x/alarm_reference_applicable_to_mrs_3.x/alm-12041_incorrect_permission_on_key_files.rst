:original_name: ALM-12041.html

.. _ALM-12041:

ALM-12041 Incorrect Permission on Key Files
===========================================

Description
-----------

The system checks whether the permission, user, and user group information about critical directories or files is normal every 5 minutes. This alarm is generated when the information is abnormal.

This alarm is cleared when the information becomes normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12041    Major          Yes
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

System functions are unavailable.

Possible Causes
---------------

The file permission is abnormal or the file is lost due to a user manually modified information such as the file permission, user, and user group, or the system is powered off unexpectedly.

Procedure
---------

**Check whether the abnormal file exists and whether the permission on the abnormal file is correct.**

#. On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms**.

#. Check the value of **HostName** to obtain the host name involved in this alarm. Check the value of **PathName** to obtain the path or name of the abnormal file.

#. Log in to the node for which the alarm is generated as user **root**.

#. Run the **ll** *pathName* command, where *pathName* indicates the name of the abnormal file to obtain the user, permission, and user group information about the file or directory.

#. .. _alm-12041__li1834285111014:

   Go to **${BIGDATA_HOME}/om-agent/nodeagent/etc/agent/autocheck** directory. Then run the **vi keyfile** command and search for the name of the abnormal file and check the due permission of the file.

   .. note::

      To ensure proper configuration synchronization between the active and standby OMS servers, files, directories, and files and sub-directories in the directories configured in **$OMS_RUN_PATH/workspace/ha/module/hasync/plugin/conf/filesync.xml** will also be monitored except files and directories in **keyfile**. User **omm** must have read and write permissions of files and read and execute permissions of directories.

#. Compare the real-world permission of the file with the due permission obtained in :ref:`5 <alm-12041__li1834285111014>` and correct the permission, user, and user group information for the file.

#. Wait a hour and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-12041__li1068683211014>`.

   .. note::

      If the disk partition where the cluster installation directory resides is used up, some temporary files will be generated in the program installation directory when running the **sed** command fails. Users do not have the read, write, and execute permissions of these temporary files. The system reports an alarm indicating that permissions of temporary files are abnormal if these files are within the monitoring range of the alarm. Perform the preceding alarm handling processes to clear the alarm. Alternatively, you can directly delete the temporary files after confirming that files with abnormal permissions are temporary. The temporary file generated after a **sed** command execution failure is similar to the following.

   |image1|

**Collect fault information.**

8.  .. _alm-12041__li1068683211014:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

9.  Select **NodeAgent** from the **Service** and click **OK**.

10. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383855.jpg
.. |image2| image:: /_static/images/en-us_image_0269383856.png
