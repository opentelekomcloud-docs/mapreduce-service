:original_name: ALM-45276.html

.. _ALM-45276:

ALM-45276 Abnormal RangerAdmin Status
=====================================

Description
-----------

The alarm module checks the RangerAdmin service status every 60 seconds. This alarm is generated if RangerAdmin is unavailable.

This alarm is automatically cleared after the RangerAdmin service recovers.

Attributes
----------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
45276    Major          Yes
======== ============== =====================

Parameters
----------

=========== =========================================
Name        Meaning
=========== =========================================
Source      Cluster for which the alarm is generated.
ServiceName Service for which the alarm is generated.
RoleName    Role for which the alarm is generated.
HostName    Host for which the alarm is generated.
=========== =========================================

Impact on the System
--------------------

If the status of a RangerAdmin is abnormal, access to the Ranger native UI is not affected. If there are two abnormal RangerAdmin instances, the Ranger native UI cannot be accessed and operations such as creating, modifying, and deleting policies are unavailable.

Possible Causes
---------------

The RangerAdmin port is not started.

Procedure
---------

**Check the port process.**

#. In the alarm list on MRS Manager, locate the row that contains the alarm, and click |image1| to view the name of the host for which the alarm is generated.

#. Log in to the node where the RangerAdmin instance is located as user **omm**. Run the **ps -ef|grep "proc_rangeradmin" \| grep -v grep \| awk -F ' ' '{print $2}'** command to obtain **pid** of the RangerAdmin process, and run the **netstat -anp|grep pid \| grep LISTEN** command to check whether the RangerAdmin process listens to port 21401 in the security mode and port 21400 in standard mode.

   -  If yes, go to :ref:`4 <alm-45276__li16749195915615>`.
   -  If no, restart the faulty RangerAdmin instance or Ranger service and go to :ref:`3 <alm-45276__li24833719161349>`.

#. .. _alm-45276__li24833719161349:

   In the alarm list, check whether the "Abnormal RangerAdmin Status" alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-45276__li16749195915615>`.

**Collect the fault information.**

4. .. _alm-45276__li16749195915615:

   On MRS Manager, choose **O&M** > **Log** > **Download**.

5. Expand the **Service** drop-down list, and select **Ranger** for the target cluster.

6. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

After the fault that triggers the alarm is rectified, the alarm is automatically cleared.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927302.png
.. |image2| image:: /_static/images/en-us_image_0000001583087289.png
