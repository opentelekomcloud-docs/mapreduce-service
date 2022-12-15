:original_name: alm_20002.html

.. _alm_20002:

ALM-20002 Hue Service Unavailable
=================================

Description
-----------

The system checks the Hue service status every 60 seconds. This alarm is generated if the Hue service is unavailable.

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
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The system cannot provide data loading, query, and extraction services.

Possible Causes
---------------

-  The KrbServer service on which Hue depends is abnormal.
-  The DBService service on which Hue depends is abnormal.
-  The network connection to DBService is abnormal.

Procedure
---------

**Check whether the KrbServer service is normal.**

#. Go to the MRS cluster details page and click **Components**.

   .. note::

      For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

#. In the service list, check whether **Health Status** of **KrbServer** is **Good**.

   -  If yes, go to :ref:`5 <alm_20002__en-us_topic_0191813890_li1965161312249>`.
   -  If no, go to :ref:`3 <alm_20002__en-us_topic_0191813890_en-us_topic_0087039274_li3201870494312>`.

#. .. _alm_20002__en-us_topic_0191813890_en-us_topic_0087039274_li3201870494312:

   Click **Restart** in the **Operation** column of the KrbServer service to restart the service.

#. Wait for several minutes. Check whether ALM-20002 Hue Service Unavailable is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm_20002__en-us_topic_0191813890_li1965161312249>`.

**Check whether DBService is normal.**

5. .. _alm_20002__en-us_topic_0191813890_li1965161312249:

   Go to the MRS cluster details page and click **Components**.

   .. note::

      For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

6. In the service list, check whether **Health Status** of **DBService** is **Good**.

   -  If yes, go to :ref:`9 <alm_20002__en-us_topic_0191813890_en-us_topic_0087039274_li3066850394312>`.
   -  If no, go to :ref:`7 <alm_20002__en-us_topic_0191813890_en-us_topic_0087039274_li6300946494312>`.

7. .. _alm_20002__en-us_topic_0191813890_en-us_topic_0087039274_li6300946494312:

   Click **Restart** in the **Operation** column of the DBService service to restart the service.

   .. note::

      To restart the service, you need to enter the password of the MRS Manager administrator and select **Start or restart related services** .

8. Wait for several minutes. Check whether ALM-20002 Hue Service Unavailable is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm_20002__en-us_topic_0191813890_en-us_topic_0087039274_li3066850394312>`.

**Check whether the network connected to DBService is normal.**

9.  .. _alm_20002__en-us_topic_0191813890_en-us_topic_0087039274_li3066850394312:

    Choose **Components** > **Hue** > **Instance** and record the IP address of the active Hue node.

10. Use PuTTY to log in to the active Hue.

11. Run the **ping** command to check whether the network connection between the host where the active Hue is located and the host where DBService is located is normal. (The method of obtaining the DBService service IP address is the same as that of obtaining the active Hue IP address.)

    -  If yes, go to :ref:`17 <alm_20002__en-us_topic_0191813890_li8901153153924>`.
    -  If no, go to :ref:`12 <alm_20002__en-us_topic_0191813890_en-us_topic_0087039274_li4180632994312>`.

12. .. _alm_20002__en-us_topic_0191813890_en-us_topic_0087039274_li4180632994312:

    Contact the network administrator to repair the network.

13. Wait for several minutes. Check whether ALM-20002 Hue Service Unavailable is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`17 <alm_20002__en-us_topic_0191813890_li8901153153924>`.

    **Collect fault information.**

14. On MRS Manager, choose **System** > **Export Log**.

15. Select the following nodes from the **Services** drop-down list and click **OK**.

    -  Hue
    -  Controller

16. Set **Start Time** and **End Time** for log collection to 10 minutes before and after the alarm is generated, select an export type, and click **OK** to collect the corresponding fault log information.

**Restart Hue.**

17. .. _alm_20002__en-us_topic_0191813890_li8901153153924:

    Choose **Components** > **Hue**.

18. Choose **More** > **Restart Service** and click **OK**.

19. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`20 <alm_20002__en-us_topic_0191813890_li572522141314>`.

20. .. _alm_20002__en-us_topic_0191813890_li572522141314:

    Collect fault information.

    a. On MRS Manager, choose **System** > **Export Log**.
    b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
