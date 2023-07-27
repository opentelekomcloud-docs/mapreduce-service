:original_name: ALM-20002.html

.. _ALM-20002:

ALM-20002 Hue Service Unavailable
=================================

Description
-----------

This alarm is generated when the Hue service is unavailable. The system checks the Hue service status every 60 seconds.

This alarm is cleared when the Hue service is normal.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
20002    Critical       Yes
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

The system cannot provide data loading, query, and extraction services.

Possible Causes
---------------

-  The internal KrbServer service on which the Hue service depends is abnormal.
-  The internal DBService service on which the Hue service depends is abnormal.
-  The network connection to the DBService is abnormal.

Procedure
---------

**Check whether the KrbServer is abnormal.**

#. On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services**. In the service list, check whether the **KrbServer** running status is **Normal**.

   -  If yes, go to :ref:`4 <alm-20002__li5904191195739>`.
   -  If no, go to :ref:`2 <alm-20002__li11299456195739>`.

#. .. _alm-20002__li11299456195739:

   Restart the KrbServer service.

#. Wait several minutes, and check whether **Hue Service Unavailable** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-20002__li5904191195739>`.

**Check whether the DBService is abnormal.**

4. .. _alm-20002__li5904191195739:

   On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services**.

5. In the service list, check whether the **DBService** running status is **Normal**.

   -  If yes, go to :ref:`8 <alm-20002__li6429027195739>`.
   -  If no, go to :ref:`6 <alm-20002__li3868925195739>`.

6. .. _alm-20002__li3868925195739:

   Restart the DBService.

   .. note::

      To restart the service, enter the FusionInsight Manager administrator password.

7. Wait several minutes, and check whether **Hue Service Unavailable** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-20002__li6429027195739>`.

**Check whether the network connection to the DBService is normal.**

8.  .. _alm-20002__li6429027195739:

    Choose **Cluster** > *Name of the desired cluster* > **Services** > **Hue** > **Instance**, record the IP address of the active Hue.

9.  Log in to the active Hue.

10. Run the **ping** command to check whether communication between the host that runs the active Hue and the hosts that run the DBService is normal. (Obtain the IP addresses of the hosts that run the DBService in the same way as that for obtaining the IP address of the active Hue.)

    -  If yes, go to :ref:`13 <alm-20002__li66042197195739>`.
    -  If no, go to :ref:`11 <alm-20002__li44855049195739>`.

11. .. _alm-20002__li44855049195739:

    Contact the administrator to restore the network.

12. Wait several minutes, and check whether **Hue Service Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-20002__li66042197195739>`.

**Collect fault information.**

13. .. _alm-20002__li66042197195739:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

14. Select the following nodes in the required cluster from the **Service** drop-down list:

    -  Hue
    -  Controller

15. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. On the FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Hue**.

17. Choose **More** > **Restart Service**, and click **OK**.

18. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`19 <alm-20002__li39514705195739>`.

19. .. _alm-20002__li39514705195739:

    Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448414.png
