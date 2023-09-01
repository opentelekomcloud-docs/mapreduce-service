:original_name: ALM-16003.html

.. _ALM-16003:

ALM-16003 Background Thread Usage Exceeds the Threshold
=======================================================

Description
-----------

The system checks the background thread usage in every 30 seconds. This alarm is generated when the usage of the background thread pool of Hive exceeds the threshold, 90% by default.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
16003    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

There are too many background threads, so the newly submitted task cannot run in time.

Possible Causes
---------------

The usage of the background thread pool of Hive is excessively high when:

-  There are many tasks executed in the background thread pool of HiveServer.
-  The capacity of the background thread pool of HiveServer is too small.

Procedure
---------

**Check the number of tasks executed in the background thread pool of HiveServer.**

#. On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive**. On the displayed page, click **HiveServer Instance** and check values of **Background Thread Count** and **Background Thread Usage**.

#. Check whether the number of background threads in the latest half an hour is excessively high. (By default, the queue number is 100, and the thread number is considered as high if it is 90 or larger.)

   -  If it is, go to :ref:`3 <alm-16003__li7203188143816>`.
   -  If it is not, go to :ref:`5 <alm-16003__li1418798143810>`.

#. .. _alm-16003__li7203188143816:

   Adjust the number of tasks submitted to the background thread pool. (For example, cancel some time-consuming tasks with low performance.)

#. Check whether the values of Background Thread Count and Background Thread Usage decrease.

   -  If it is, go to :ref:`7 <alm-16003__li73422961119>`.
   -  If it is not, go to :ref:`5 <alm-16003__li1418798143810>`.

**Check the capacity of the HiveServer background thread pool.**

5. .. _alm-16003__li1418798143810:

   On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive**. On the displayed page, click **HiveServer Instance** and check values of Background Thread Count and Background Thread Usage.

6. Increase the value of **hive.server2.async.exec.threads** in the **${BIGDATA_HOME}/FusionInsight_HD\_8.1.0.1/1_23_HiveServer/etc/hive-site.xml** file. For example, increase the value by 20%.

7. .. _alm-16003__li73422961119:

   Save the modification.

8. Check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`9 <alm-16003__li3112518015571>`.

**Collect fault information.**

9.  .. _alm-16003__li3112518015571:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

10. Select **Hive** in the required cluster from the **Service**.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087477.png
