:original_name: ALM-45653.html

.. _ALM-45653:

ALM-45653 Invalid Flink HA Certificate File
===========================================

This section applies to MRS 3.3.0 or later.

Alarm Description
-----------------

Flink checks whether the HA certificate file is valid (whether the certificate exists and whether its format is correct) in the first health check or at 01:00:00 every day. This alarm is generated when the certificate file is invalid. This alarm is automatically cleared when the certificate file becomes valid again.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45653    Major          Yes
======== ============== ============

Alarm Parameters
----------------

=========== =======================================================
Parameter   Description
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

Some functions are unavailable.

Possible Causes
---------------

The HA certificate file is invalid.

Handling Procedure
------------------

**View alarm information.**

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms** > **ALM-45653 Invalid Flink HA Certificate File**, view **Location**, obtain the name of the host for which the alarm is generated, and click the host name to view its IP address.

**Check whether the HA certificate file in the system is valid.**

2. Log in to the host for which the alarm is generated as user **omm**.

3. Run the **cd ${BIGDATA_HOME}/FusionInsight_Flink_*/install/FusionInsight-Flink-*/ha/local/cert** command to go to the directory where the HA certificate is stored.

4. Run the **ls -l** command to check whether the **server.crt** file exists.

   -  If yes, go to :ref:`5 <alm-45653__li224142155111>`.
   -  If no, go to :ref:`6 <alm-45653__li2241132105116>`.

5. .. _alm-45653__li224142155111:

   Run the **openssl x509 -in server.crt -text -noout** command and check whether the command output is normal.

   -  If yes, go to :ref:`9 <alm-45653__li593632253716>`.
   -  If no, go to :ref:`6 <alm-45653__li2241132105116>`.

6. .. _alm-45653__li2241132105116:

   Run the **cd** **${BIGDATA_HOME}/FusionInsight_Flink_*/install/FusionInsight-Flink-*/flink/sbin** command to go to the Flink script directory.

7. Run the **sh proceed_ha_ssl_cert.sh** command to generate a new HA certificate. Then, check whether the alarm is cleared 1 minute later.

   -  If yes, go to :ref:`8 <alm-45653__li57811511185514>`.
   -  If no, go to :ref:`9 <alm-45653__li593632253716>`.

8. .. _alm-45653__li57811511185514:

   Check whether this alarm is generated again during periodic system check.

   -  If yes, go to :ref:`9 <alm-45653__li593632253716>`.
   -  If no, no further action is required.

**Collect fault information.**

9.  .. _alm-45653__li593632253716:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the **Service** drop-down list, and select **Flink** for the target cluster.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000001971648854.png
