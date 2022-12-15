:original_name: alm_18010.html

.. _alm_18010:

ALM-18010 Number of Pending Yarn Tasks Exceeds the Threshold
============================================================

Description
-----------

The system checks the number of pending Yarn tasks every 30 seconds and compares the number of tasks with the threshold. This alarm is generated when the number of pending tasks exceeds the threshold.

You can change the threshold by choosing **System** > **Configure Alarm Threshold** > **Service** > **Yarn** > **Queue Root Pending Applications** > **Queue Root Pending Applications** on MRS Manager.

This alarm is cleared when the number of pending tasks is less than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
18010    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------+---------------------------------------------------------+
| Parameter         | Description                                             |
+===================+=========================================================+
| ServiceName       | Specifies the service for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

Tasks may be stacked and cannot be processed in a timely manner.

Possible Causes
---------------

The computing capability of the cluster is lower than the task submission rate. As a result, the task cannot be processed in a timely manner after being submitted.

Procedure
---------

#. Check the usage of memory and vCores on the Yarn page.

   Check whether the values of **Memory Used|Memory Total** and **VCores Used|VCores Total** on the native Yarn page reach or approach the maximum values.

   -  If yes, go to :ref:`2 <alm_18010__en-us_topic_0227101889_li181801656143013>`.
   -  If no, go to :ref:`5 <alm_18010__en-us_topic_0227101889_li572522141314>`.

#. .. _alm_18010__en-us_topic_0227101889_li181801656143013:

   Check the number of submitted tasks.

   Check whether the running tasks are submitted at a normal frequency.

   -  If yes, go to :ref:`3 <alm_18010__en-us_topic_0227101889_li10509161210322>`.
   -  If no, go to :ref:`5 <alm_18010__en-us_topic_0227101889_li572522141314>`.

#. .. _alm_18010__en-us_topic_0227101889_li10509161210322:

   Scale out the cluster.

   The scale-out is based on the site requirements. For details, see :ref:`Manually Scaling Out a Cluster <mrs_01_0041>`.

#. After the scale-out is completed, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm_18010__en-us_topic_0227101889_li572522141314>`.

#. .. _alm_18010__en-us_topic_0227101889_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
