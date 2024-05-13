:original_name: ALM-12053.html

.. _ALM-12053:

ALM-12053 Host File Handle Usage Exceeds the Threshold
======================================================

Description
-----------

The system checks the file handle usage every 30 seconds and compares the actual usage with the threshold (the default threshold is 80%). This alarm is generated when the host file handle usage exceeds the threshold for several times (5 times by default) consecutively.

To change the threshold, choose **O&M > Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Host Status** > **Host File Handle Usage**.

When the **Trigger Count** is 1, this alarm is cleared when the host file handle usage is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the host file handle usage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12053    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated.                                                            |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

The I/O operations, such as opening a file or connecting to network, cannot be performed and programs are abnormal.

Possible Causes
---------------

-  The application process is abnormal. For example, the opened file or socket is not closed.
-  The number of file handles cannot meet the current service requirements.
-  The system is abnormal.

Procedure
---------

**Check information about files opened in processes.**

#. On MRS Manager, click |image1| in the row where the alarm is located in the real-time alarm list and obtain the IP address of the host for which the alarm is generated.

#. Log in to the host for which the alarm is generated as user **root**.

#. Run the **lsof -n|awk '{print $2}'|sort|uniq -c|sort -nr|more** command to check the process that occupies excessive file handles.

#. Check whether the processes in which a large number of files are opened are normal. For example, check whether there are files or sockets not closed.

   -  If yes, go to :ref:`5 <alm-12053__li698311306446>`.
   -  If no, go to :ref:`7 <alm-12053__li50842733151924>`.

#. .. _alm-12053__li698311306446:

   Release the abnormal processes that occupy too many file handles.

#. Five minutes later, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-12053__li50842733151924>`.

**Increase the number of file handles.**

7.  .. _alm-12053__li50842733151924:

    On MRS Manager, click |image2| in the row where the alarm is located in the real-time alarm list and obtain the IP address of the host for which the alarm is generated.

8.  Log in to the host for which the alarm is generated as user **root**.

9.  .. _alm-12053__li103121715194518:

    Contact the system administrator to increase the number of system file handles.

10. Run the **cat /proc/sys/fs/file-nr** command to view the used handles and the maximum number of file handles. The first value is the number of used handles, the third value is the maximum number. Please check whether the usage exceeds the threshold.

    -  If yes, go to :ref:`9 <alm-12053__li103121715194518>`.

    -  If no, go to :ref:`11 <alm-12053__li133010151924>`.

       .. code-block::

          # cat /proc/sys/fs/file-nr
          12704 0 640000

11. .. _alm-12053__li133010151924:

    Wait for 5 minutes, and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-12053__li21666806151924>`.

**Check whether the system environment is abnormal.**

12. .. _alm-12053__li21666806151924:

    Contact the system administrator to check whether the operating system is abnormal.

    -  If yes, go to :ref:`13 <alm-12053__li23370043151924>` to rectify the fault.
    -  If no, go to :ref:`14 <alm-12053__li58218801151924>`.

13. .. _alm-12053__li23370043151924:

    Wait for 5 minutes, and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-12053__li58218801151924>`.

**Collect fault information.**

14. .. _alm-12053__li58218801151924:

    On the MRS Manager home page of the active cluster, choose **O&M** > **Log > Download**.

15. Select **OMS** from the **Service** and click **OK**.

16. Set **Host** to the node for which the alarm is generated and the active OMS node.

17. Click |image3| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

18. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927418.png
.. |image2| image:: /_static/images/en-us_image_0000001532607746.png
.. |image3| image:: /_static/images/en-us_image_0000001582927641.png
