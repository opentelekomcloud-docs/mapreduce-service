:original_name: ALM-45654.html

.. _ALM-45654:

ALM-45654 Flink HA Certificate Is About to Expire
=================================================

This section applies to MRS 3.3.0 or later.

Alarm Description
-----------------

Flink checks whether the HA certificate file is about to expire in the first health check or at 01:00:00 every day. This alarm is generated when the remaining validity period is less than or equal to 30 days. This alarm is automatically cleared when the remaining validity period is greater than 30 days.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45654    Major          Yes
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

Currently, there is no impact on the system.

Possible Causes
---------------

The HA certificate is about to expire.

Handling Procedure
------------------

**View alarm information.**

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms** > **ALM-45654 Flink HA Certificate Is About to Expire**, view **Location**, obtain the name of the host for which the alarm is generated, and click the host name to view its IP address.

**Check whether the HA certificate file in the system is valid. If it is not, generate a new one.**

2. Log in to the host for which the alarm is generated as user **omm**.

3. Run the **cd ${BIGDATA_HOME}/FusionInsight_Flink_*/install/FusionInsight-Flink-*/ha/local/cert** command to go to the directory where the HA certificate is stored.

4. Run the **openssl x509 -noout -text -in server.crt** command to query the effective time and due time of the HA certificate.

5. Perform :ref:`6 <alm-45654__li99371922103716>` to :ref:`7 <alm-45654__li16937182293715>` during off-peak hours to update the certificate file as needed.

6. .. _alm-45654__li99371922103716:

   Run the **cd** **${BIGDATA_HOME}/FusionInsight_Flink_*/install/FusionInsight-Flink-*/flink/sbin** command to go to the Flink script directory.

7. .. _alm-45654__li16937182293715:

   Run the **sh proceed_ha_ssl_cert.sh** command to generate a new HA certificate. Then, check whether the alarm is cleared 1 minute later.

   -  If yes, go to :ref:`9 <alm-45654__li127861713811>`.
   -  If no, go to :ref:`8 <alm-45654__li6673192244411>`.

8. .. _alm-45654__li6673192244411:

   On the node where the standby FlinkServer instance is located, repeat :ref:`6 <alm-45654__li99371922103716>` to :ref:`7 <alm-45654__li16937182293715>`. Then, check whether the alarm is cleared 1 minute later.

   -  If yes, go to :ref:`9 <alm-45654__li127861713811>`.
   -  If no, go to :ref:`10 <alm-45654__li593632253716>`.

9. .. _alm-45654__li127861713811:

   Check whether this alarm is generated again during periodic system check.

   -  If yes, go to :ref:`10 <alm-45654__li593632253716>`.
   -  If no, no further action is required.

**Collect fault information.**

10. .. _alm-45654__li593632253716:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Expand the **Service** drop-down list, and select **Flink** for the target cluster.

12. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002008129165.png
