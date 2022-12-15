:original_name: ALM-12034.html

.. _ALM-12034:

ALM-12034 Periodical Backup Failure
===================================

Description
-----------

The system executes the periodic backup task every 60 minutes. This alarm is generated when a periodical backup task fails to be executed. This alarm is cleared when the next backup task is executed successfully.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12034    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| TaskName    | Specifies the task.                                               |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

There are not available backup packages for a long time, so the system cannot be restored in case of exceptions.

Possible Causes
---------------

The alarm cause depends on the task details. Handle the alarm according to the logs and alarm details.

Procedure
---------

**Check whether the disk space is sufficient.**

#. In the FusionInsight Manager portal, click **O&M > Alarm > Alarms**.

#. In the alarm list, click |image1| in the row where the alarm is located and obtain **TaskName** from **Location**.

#. Choose **O&M** > **Backup and Restoration > Backup Management**.

#. Search for the backup task based on **TaskName** and click **More** in the **Operation** column. In the displayed dialog box, click **View History** and view the task details.

#. In the displayed dialog box and click |image2| to check whether the following message is displayed: Failed to backup xx due to insufficient disk space, move the data in the xx directory to other directories.

   -  If yes, go to :ref:`6 <alm-12034__li8265923133114>`.
   -  If no, go to :ref:`13 <alm-12034__li115006411351>`.

#. .. _alm-12034__li8265923133114:

   Choose **Backup Path** > **View** and obtain the **Backup Path**.

#. Log in to the node as user **root** and run the following command to check the node mounting details:

   **df -h**

#. Check whether the available space of the node to which the backup path is mounted is less than 20 GB.

   -  If yes, go to :ref:`9 <alm-12034__li181154133220>`.
   -  If no, go to :ref:`13 <alm-12034__li115006411351>`.

#. .. _alm-12034__li181154133220:

   Check whether there are many backup packages in the backup directory.

   -  If yes, go to :ref:`10 <alm-12034__li3795101373317>`.
   -  If no, go to :ref:`13 <alm-12034__li115006411351>`.

#. .. _alm-12034__li3795101373317:

   Enable the available space of the node to which the backup directory is mounted to be greater than 20 GB by moving backup packages out of the backup directory or delete the backup packages.

#. After the problem is resolved, perform the backup task again and check whether the backup task execution is successful.

   -  If yes, go to :ref:`12 <alm-12034__li5916521794522>`.
   -  If no, go to :ref:`13 <alm-12034__li115006411351>`.

#. .. _alm-12034__li5916521794522:

   After 2 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`13 <alm-12034__li115006411351>`.

**Collect fault information.**

13. .. _alm-12034__li115006411351:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

14. Select **Controller** from the **Service** and click **OK**.

15. Click |image3| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383843.png
.. |image2| image:: /_static/images/en-us_image_0000001127057881.png
.. |image3| image:: /_static/images/en-us_image_0269383844.png
