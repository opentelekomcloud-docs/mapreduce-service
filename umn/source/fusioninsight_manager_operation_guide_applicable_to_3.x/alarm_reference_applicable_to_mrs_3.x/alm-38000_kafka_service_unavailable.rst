:original_name: ALM-38000.html

.. _ALM-38000:

ALM-38000 Kafka Service Unavailable
===================================

Description
-----------

The system checks the Kafka service status every 30 seconds. This alarm is generated when the Kafka service is unavailable.

This alarm is cleared when the Kafka service recovers.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
38000    Critical       Yes
======== ============== =====================

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The cluster cannot provide the Kafka service, and users cannot perform new Kafka tasks.

Possible Causes
---------------

-  The KrbServer service is abnormal.(Skip this step if the normal mode is used.)
-  The ZooKeeper service is abnormal or does not respond.
-  The Broker instance in the Kafka cluster are abnormal.

Procedure
---------

**Check the status of the KrbServer service. (Skip this step if the normal mode is used.)**

#. On the FusionInsight Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services > KrbServer**.

#. .. _alm-38000__li9636121161118:

   Check whether the running status of the KrbServer service is **Normal**.

   -  If yes, go to :ref:`5 <alm-38000__li23201109161118>`.
   -  If no, go to :ref:`3 <alm-38000__li42328297161118>`.

#. .. _alm-38000__li42328297161118:

   Rectify the fault by following the steps provided in **ALM-25500 KrbServer Service Unavailable**.

#. Perform :ref:`2 <alm-38000__li9636121161118>` again.

**Check the status of the ZooKeeper cluster.**

5. .. _alm-38000__li23201109161118:

   Check whether the running status of the ZooKeeper service is **Normal**.

   -  If yes, go to :ref:`8 <alm-38000__li29459861161118>`.
   -  If no, go to :ref:`6 <alm-38000__li241672161118>`.

6. .. _alm-38000__li241672161118:

   If ZooKeeper service is stopped, start it, else rectify the fault by following the steps provided in **ALM-13000 ZooKeeper Service Unavailable**.

7. Perform :ref:`5 <alm-38000__li23201109161118>` again.

**Check the Broker status.**

8.  .. _alm-38000__li29459861161118:

    Choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance** to go to the Kafka instances page.

9.  Check whether all instances in **Roles** are running properly.

    -  If yes, go to :ref:`11 <alm-38000__li65780611161118>`.
    -  If no, go to :ref:`10 <alm-38000__li1856436161118>`.

10. .. _alm-38000__li1856436161118:

    Select all Broker instances, choose **More** > **Restart Instance**, and check whether the instances restart successfully.

    -  If yes, go to :ref:`11 <alm-38000__li65780611161118>`.
    -  If no, go to :ref:`13 <alm-38000__li62186744161118>`.

11. .. _alm-38000__li65780611161118:

    Choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** to check whether the running status is **Normal**.

    -  If yes, go to :ref:`12 <alm-38000__li30279690161118>`.
    -  If no, go to :ref:`13 <alm-38000__li62186744161118>`.

12. .. _alm-38000__li30279690161118:

    Wait for 30 seconds and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-38000__li62186744161118>`.

**Collecting Fault Information**

13. .. _alm-38000__li62186744161118:

    On the FusionInsight Manager portal, choose **O&M** > **Log** > **Download**.

14. Select **Kafka** in the required cluster from the **Service** drop-down list.

15. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417499.png
