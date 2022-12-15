:original_name: alm_12034.html

.. _alm_12034:

ALM-12034 Periodic Backup Failure
=================================

Description
-----------

This alarm is generated when a periodic backup task fails to be executed. This alarm is cleared when the next backup task is executed successfully.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12034    Major          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
TaskName    Specifies the task name.
=========== =======================================================

Impact on the System
--------------------

No backup package is available for a long time, so the system cannot be restored in case of exceptions.

Possible Causes
---------------

The alarm cause depends on the task details. Handle the alarm according to the logs and alarm details.

Procedure
---------

**Checking whether the disk space is insufficient**

#. On MRS Manager, choose **Alarms**.

#. In the alarm list, click |image1| of the alarm and obtain the task name from the **Location** area.

#. Choose **System** > **Back Up Data**.

#. Search for the backup task based on the task name and choose **More** > **View History** in the **Operation** column to view detailed information about the backup task.

#. Choose **Details** > **View** and check whether message "Failed to backup xx due to insufficient disk space, move the data in the /srv/BigData/LocalBackup directory to other directories." exists.

   -  If yes, go to :ref:`6 <alm_12034__li347718556387>`.
   -  If no, go to :ref:`13 <alm_12034__li164761155133811>`.

#. .. _alm_12034__li347718556387:

   Choose **Backup Path** > **View** to obtain the backup path.

#. Log in to the node as user **root** and view the mounting details of the node.

   **df -h**

#. Check whether the available space of the node to which the backup path is mounted is less than 20 GB.

   -  If yes, go to :ref:`9 <alm_12034__li74787554389>`.
   -  If no, go to :ref:`13 <alm_12034__li164761155133811>`.

#. .. _alm_12034__li74787554389:

   Check whether the backup package exists in the backup directory and whether the available space of the node to which the backup directory is mounted is less than 20 GB.

   -  If yes, go to :ref:`10 <alm_12034__li1847855563815>`.
   -  If no, go to :ref:`13 <alm_12034__li164761155133811>`.

#. .. _alm_12034__li1847855563815:

   Ensure that the available space of the node to which the backup directory is mounted to be greater than 20 GB by moving backup packages out of the backup directory or deleting the backup packages.

#. Start the backup task again and check whether the backup task is executed.

   -  If yes, go to :ref:`12 <alm_12034__li104790555386>`.
   -  If no, go to :ref:`13 <alm_12034__li164761155133811>`.

#. .. _alm_12034__li104790555386:

   After 2 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`13 <alm_12034__li164761155133811>`.

**Collecting fault information**

13. .. _alm_12034__li164761155133811:

    On MRS Manager, choose **System** > **Export Log**.

14. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Reference
---------

None

.. |image1| image:: /_static/images/en-us_image_0000001296058020.png
