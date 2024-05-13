:original_name: ALM-23003.html

.. _ALM-23003:

ALM-23003 Loader Task Execution Failure
=======================================

Description
-----------

This alarm is generated immediately when the system detects that the Loader job fails. This alarm is cleared when the failed job is manually handled by a user. This alarm must be manually cleared.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
23003    Minor          No
======== ============== =====================

Parameters
----------

=========== ===========================================================
Name        Meaning
=========== ===========================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
JobID       Specifies the ID of failed Loader job.
JobName     Specifies the failed Loader job.
UserName    Specifies the name of the user who submits the Loader job.
Details     Supplementary information for which the alarm is generated.
=========== ===========================================================

Impact on the System
--------------------

An exception occurs during the execution of the submitted Loader job, and the execution fails. No execution result can be obtained. Execute the job again after rectifying the fault.

Possible Causes
---------------

-  Task parameters are incorrectly configured.
-  Exceptions occur when Yarn is executing a job.

Procedure
---------

**Check whether task parameters are incorrectly configured.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms** and click the alarm drop-down list from the alarm list, obtain the **Alarm Cause**.
#. If the alarm cause is "Failure to submit job", view error details in **Additional Information**, and go to the Loader WebUI to view the execution history of the job.

   .. note::

      By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

#. Submit the task again.
#. Check whether the task executed successfully.

   -  If yes, go to :ref:`9 <alm-23003__li4574774083922>`.
   -  If no, go to :ref:`5 <alm-23003__li4864190683922>`.

**Check whether exceptions occur when Yarn is executing a job.**

5. .. _alm-23003__li4864190683922:

   On MRS Manager, click the alarm drop-down list from the alarm list, obtain the **Alarm Cause**.

6. Check whether the Yarn activity is executed properly in the **Alarm Cause**. If the alarm cause is "Yarn execution failed", the Yarn activity is abnormal.

   -  If yes, go to :ref:`7 <alm-23003__li4550592983922>`.
   -  If no, go to :ref:`10 <alm-23003__li6410647583922>`.

7. .. _alm-23003__li4550592983922:

   Submit the task again.

8. Please check whether the task executed successfully.

   -  If yes, go to :ref:`9 <alm-23003__li4574774083922>`.
   -  If no, go to :ref:`10 <alm-23003__li6410647583922>`.

9. .. _alm-23003__li4574774083922:

   In the alarm list, click **Clear** from **Operation** to manually clear the alarm. No further action is required.

**Collect fault information.**

10. .. _alm-23003__li6410647583922:

    On MRS Manager, choose **O&M** > **Log** > **Download**.

11. Select the following nodes in the required cluster from the **Service** drop-down list:

    -  DBService
    -  HDFS
    -  Loader
    -  Mapreduce
    -  Yarn
    -  ZooKeeper

12. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system does not automatically clear this alarm, and you need to manually clear the alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607822.png
