:original_name: ALM-12011.html

.. _ALM-12011:

ALM-12011 Manager Data Synchronization Exception Between the Active and Standby Nodes
=====================================================================================

Description
-----------

The system checks data synchronization between the active and standby Manager nodes every 60 seconds. This alarm is generated when the standby Manager fails to synchronize files with the active Manager.

This alarm is cleared when the standby Manager synchronizes files with the active Manager.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12011    Critical       Yes
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

Impact on the System
--------------------

Some configurations will be lost after an active/standby switchover because the configuration files on the standby Manager are not updated. Maybe Manager and some components cannot run properly.

Possible Causes
---------------

-  The link between the active and standby Managers is interrupted or The storage space of the **/srv/BigData/LocalBackup** directory is full.
-  The synchronization file does not exist or the file permission is incorrect.

Procedure
---------

**Check whether the network between the active Manager server and the standby Manager server is normal.**

#. In the FusionInsight Manager portal, click **O&M > Alarm > Alarms**, click |image1| in the row where the alarm is located and obtain the standby Manager server IP address (Peer Manager IP address) in the alarm details.

#. Log in to the active Manager server as user **root**.

#. Run the **ping** *standby Manager IP address* command to check whether the standby Manager server is reachable.

   -  If yes, go to :ref:`6 <alm-12011__li983315367129>`.
   -  If no, go to :ref:`4 <alm-12011__li3033024171750>`.

#. .. _alm-12011__li3033024171750:

   Contact the network administrator to check whether the network is faulty.

   -  If yes, go to :ref:`5 <alm-12011__li52745930171750>`.
   -  If no, go to :ref:`6 <alm-12011__li983315367129>`.

#. .. _alm-12011__li52745930171750:

   Rectify the network fault and check whether the alarm is cleared from the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12011__li983315367129>`.

**Check whether the storage space of the** **/srv/BigData/LocalBackup** **directory is full.**

6. .. _alm-12011__li983315367129:

   Run the following command to check whether the storage space of the **/srv/BigData/LocalBackup** directory is full:

   **df -hl /srv/BigData/LocalBackup**

   -  If yes, go to :ref:`7 <alm-12011__li11402194014150>`.
   -  If no, go to :ref:`10 <alm-12011__li1826164817917>`.

7. .. _alm-12011__li11402194014150:

   Run the following command to clear unnecessary backup files:

   **rm -rf** *Directory to be cleared*

   Example:

   **rm -rf** **/srv/BigData/LocalBackup/0/default-oms_20191211143443**

8. On FusionInsight Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

   In the **Operation** column of the backup task to be performed, click **Configure** and change the value of **Maximum Number of Backup Copies** to reduce the number of backup file sets.

9. Wait about 1 minute and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-12011__li1826164817917>`.

**Check whether the synchronization file exists and whether the file permission is normal.**

10. .. _alm-12011__li1826164817917:

    Run the following command to check whether the synchronization file exists.

    **find /srv/BigData/ -name "sed*"**

    **find /opt -name "sed*"**

    -  If yes, go to :ref:`11 <alm-12011__li1926214814915>`.
    -  If no, go to :ref:`12 <alm-12011__li192637482095>`.

11. .. _alm-12011__li1926214814915:

    Run the following command to view the synchronization file information and permission obtained in :ref:`10 <alm-12011__li1826164817917>`.

    **ll** *path of the file to be found*

    -  If the size of the file is 0 and the permission column is **-**, the file is a junk file. Run the following command to delete it.

       **rm -rf** *files to be deleted*

       Wait for several minutes and check whether the alarm is cleared. If the alarm persists, go to :ref:`12 <alm-12011__li192637482095>`.

    -  If the file size is not 0, go to :ref:`12 <alm-12011__li192637482095>`.

12. .. _alm-12011__li192637482095:

    View the log files generated when the alarm is generated.

    a. Run the following command to switch to the HA run log file path.

       **cd /var/log/Bigdata/omm/oms/ha/runlog**/

    b. Decompress and view the log files generated when the alarm is generated.

       For example, if the name of the file to be viewed is **ha.log.2021-03-22_12-00-07.gz**, run the following command:

       **gunzip** *ha.log.2021-03-22_12-00-07.gz*

       **vi** *ha.log.2021-03-22_12-00-07*

       Check whether error information is reported before and after the alarm generation time.

       -  If yes, rectify the fault based on the error information. Then go to :ref:`13 <alm-12011__li985632952514>`.

          For example, if the following error information is displayed, the directory permission is insufficient. In this case, change the directory permission to be the same as that on the normal node.

          |image2|

       -  If no, go to :ref:`14 <alm-12011__li65512922171750>`.

13. .. _alm-12011__li985632952514:

    Wait about 10 minute and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-12011__li65512922171750>`.

**Collect fault information.**

14. .. _alm-12011__li65512922171750:

    On the FusionInsight Manager, choose **O&M** > **Log > Download**.

15. Select the following nodes from the **Service** and click **OK**:

    -  OmmServer
    -  Controller
    -  NodeAgent

16. Click |image3| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

17. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607938.png
.. |image2| image:: /_static/images/en-us_image_0000001583087593.png
.. |image3| image:: /_static/images/en-us_image_0000001582927829.png
