:original_name: ALM-45655.html

.. _ALM-45655:

ALM-45655 Flink HA Certificate File Has Expired
===============================================

This section applies to MRS 3.3.0 or later.

Alarm Description
-----------------

Flink checks whether the HA certificate file has expired in the first health check or at 01:00:00 every day. This alarm is generated when the HA certificate has expired. This alarm is automatically cleared when the certificate file becomes valid again.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45655    Major          Yes
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

The HA certificate file has expired.

Handling Procedure
------------------

**View alarm information.**

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms** > **ALM-45655 Flink HA Certificate File Has Expired**, view **Location**, obtain the name of the host for which the alarm is generated, and click the host name to view its IP address.

**Check whether the HA certificate file in the system is valid. If it is not, generate a new one.**

2. Log in to the host for which the alarm is generated as user **omm**.

3. Run the **cd ${BIGDATA_HOME}/FusionInsight_Flink_*/install/FusionInsight-Flink-*/ha/local/cert** command to go to the directory where the HA certificate is stored.

4. Run the **openssl x509 -noout -text -in server.crt** command to query the effective time and due time of the HA certificate and check whether the HA certificate file is valid.

   -  If yes, go to :ref:`9 <alm-45655__li593632253716>`.
   -  If no, go to :ref:`5 <alm-45655__li99371922103716>`.

5. .. _alm-45655__li99371922103716:

   Run the **cd** **${BIGDATA_HOME}/FusionInsight_Flink_*/install/FusionInsight-Flink-*/flink/sbin** command to go to the Flink script directory.

6. .. _alm-45655__li201623392391:

   Run the **sh proceed_ha_ssl_cert.sh** command to generate a new HA certificate. Then, check whether the alarm is cleared 1 minute later.

   -  If yes, go to :ref:`8 <alm-45655__li1788491915716>`.
   -  If no, go to :ref:`7 <alm-45655__li172496117507>`.

7. .. _alm-45655__li172496117507:

   On the node where the standby FlinkServer instance is located, repeat :ref:`5 <alm-45655__li99371922103716>` to :ref:`6 <alm-45655__li201623392391>`. Then, check whether the alarm is cleared 1 minute later.

   -  If yes, go to :ref:`8 <alm-45655__li1788491915716>`.
   -  If no, go to :ref:`9 <alm-45655__li593632253716>`.

8. .. _alm-45655__li1788491915716:

   Check whether this alarm is generated again during periodic system check.

   -  If yes, go to :ref:`9 <alm-45655__li593632253716>`.
   -  If no, no further action is required.

**Collect fault information.**

9.  .. _alm-45655__li593632253716:

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

.. |image1| image:: /_static/images/en-us_image_0000001971808622.png
