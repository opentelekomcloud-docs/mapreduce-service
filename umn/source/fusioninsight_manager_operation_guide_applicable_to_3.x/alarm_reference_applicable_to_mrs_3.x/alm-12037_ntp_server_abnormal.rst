:original_name: ALM-12037.html

.. _ALM-12037:

ALM-12037 NTP Server Abnormal
=============================

Description
-----------

The system checks the NTP server status every 60 seconds. This alarm is generated when the system detects that the NTP server is abnormal for 10 consecutive times.

This alarm is cleared when the NTP server recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12037    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+------------------------------------------------------------------------------+
| Name        | Meaning                                                                      |
+=============+==============================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated.            |
+-------------+------------------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.                      |
+-------------+------------------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.                         |
+-------------+------------------------------------------------------------------------------+
| HostName    | Specifies the IP address of the NTP server for which the alarm is generated. |
+-------------+------------------------------------------------------------------------------+

Impact on the System
--------------------

The NTP server configured on the active OMS node is abnormal. In this case, the active OMS node cannot synchronize time with the NTP server and a time offset may be generated in the cluster.

Possible Causes
---------------

-  The NTP server network is abnormal.
-  The NTP server authentication fails.
-  The NTP server time cannot be obtained.
-  The time obtained from the NTP server is not continuously updated.

Procedure
---------

**Check the NTP server network.**

#. On the FusionInsight Manager portal, click **O&M > Alarm > Alarms** and click |image1| in the row where the alarm is located.

#. View the alarm additional information to check whether the NTP server fails to be pinged.

   -  If yes, go to :ref:`3 <alm-12037__li601372919523>`.
   -  If no, go to :ref:`4 <alm-12037__li392824159523>`.

#. .. _alm-12037__li601372919523:

   Contact the network administrator to check the network configuration and ensure that the network between the NTP server and the active OMS node is normal. Then, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-12037__li392824159523>`.

**Check whether the NTP server authentication fails.**

4. .. _alm-12037__li392824159523:

   Log in to the active OMS node as user **root**.

5. .. _alm-12037__li24978126120:

   Run the following command to check the status of the resources on the active and standby nodes:

   **su - omm**

   **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh**

   -  If "chrony" is displayed in the **ResName** column of the command output, go to :ref:`6 <alm-12037__li179951620123417>`.
   -  If "ntp" is displayed in the **ResName** column, go to :ref:`7 <alm-12037__li650965649523>`.

   .. note::

      If both "chrony" and "ntp" are displayed in the **ResName** column of the command output, the NTP service mode is being switched. Wait for 10 minutes and perform :ref:`5 <alm-12037__li24978126120>` again. If both "chrony" and "ntp" still exist in the **ResName** column, contact O&M personnel.

6. .. _alm-12037__li179951620123417:

   Run the command **chronyc sources** to check whether the NTP server authentication fails.

   If the value of **Reach** for chrony is **0**, the connection or authentication fails.

   -  If yes, go to :ref:`12 <alm-12037__li654599509523>`.
   -  If no, go to :ref:`8 <alm-12037__li282496949523>`.

7. .. _alm-12037__li650965649523:

   Run the command **ntpq -np** to check whether the NTP server authentication fails.

   If **refid** of the NTP server is **.AUTH.**, the authentication fails.

   -  If yes, go to :ref:`12 <alm-12037__li654599509523>`.
   -  If no, go to :ref:`8 <alm-12037__li282496949523>`.

**Check whether the time can be obtained from the NTP server.**

8. .. _alm-12037__li282496949523:

   View the alarm additional information to check whether the time can be obtained from the NTP server.

   -  If yes, go to :ref:`9 <alm-12037__li549211539523>`.
   -  If no, go to :ref:`10 <alm-12037__li301460699523>`.

9. .. _alm-12037__li549211539523:

   Contact the provider of the NTP server to rectify the NTP server fault. After the NTP server is normal, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-12037__li301460699523>`.

**Check whether the time obtained from the NTP server is not continuously updated.**

10. .. _alm-12037__li301460699523:

    View the alarm additional information to check whether the time obtained from the NTP server is not continuously updated.

    -  If yes, go to :ref:`11 <alm-12037__li251290419523>`.
    -  If no, go to :ref:`12 <alm-12037__li654599509523>`.

11. .. _alm-12037__li251290419523:

    Contact the provider of the NTP server to rectify the NTP server fault. After the NTP server is normal, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-12037__li654599509523>`.

**Collect fault information.**

12. .. _alm-12037__li654599509523:

    On the FusionInsight Manager, choose **O&M** > **Log > Download**.

13. Select **NodeAgent** and **OmmServer** from the **Service** and click **OK**.

14. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

15. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607750.png
.. |image2| image:: /_static/images/en-us_image_0000001582927645.png
