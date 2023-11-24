:original_name: ALM-24014.html

.. _ALM-24014:

ALM-24014 Flume MonitorServer Certificate Is About to Expire
============================================================

This section applies to MRS 3.2.0-LTS.2 or later.

Description
-----------

MonitorServer checks whether its certificate file is about to expire every hour. This alarm is generated when the remaining validity period is at most 30 days. This alarm is automatically cleared when the remaining validity period is greater than 30 days.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24014    Major          Yes
======== ============== ==========

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

Currently, there is no impact on the system.

Possible Causes
---------------

The MonitorServer certificate file is about to expire.

Procedure
---------

**View alarm information.**

#. Log in to FusionInsight Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing **ALM-24014 MonitorServer Certificate Is About to Expire**, and view the **Location** information. View the IP address of the instance for which the alarm is generated.

**Check whether the certificate file in the system is valid. If it is not, generate a new one.**

2. Log in to the node for which the alarm is generated as user **root** and run the **su - omm** command to switch to user **omm**.

3. Run the following command to go to the MonitorServer certificate file directory:

   **cd ${BIGDATA_HOME}/FusionInsight_Porter_*/install/FusionInsight-Flume-*/flume/conf**

4. Run the following command to check the effective time and expiration time of the MonitorServer user certificate:

   **openssl x509 -noout -text -in ms_sChat.crt**

5. Perform :ref:`6 <alm-24014__li368813032118>` to :ref:`7 <alm-24014__li153512414216>` during off-peak hours to update the certificate file as needed.

6. .. _alm-24014__li368813032118:

   Run the following command to go to the Flume script directory:

   **cd ${BIGDATA_HOME}/FusionInsight_Porter_*/install/FusionInsight-Flume-*/flume/bin**

7. .. _alm-24014__li153512414216:

   Run the following command to generate a new certificate file. Then check whether the alarm is automatically cleared one hour later.

   **sh geneJKS.sh -m** *Custom password of the MonitorServer certificate on the server* **-n** *Custom password of the MonitorServer certificate on the client*

   -  If yes, go to :ref:`9 <alm-24014__li127861713811>`.
   -  If no, go to :ref:`8 <alm-24014__li6673192244411>`.

      .. note::

         The custom certificate passwords must meet the following complexity requirements:

         -  Contain at least four types of uppercase letters, lowercase letters, digits, and special characters.
         -  Contain 8 to 64 characters.
         -  Be changed periodically (for example, every three months), and certificates and trust lists are generated again to ensure security.

8. .. _alm-24014__li6673192244411:

   Log in to the Flume node for which the alarm is generated as user **omm** and repeat :ref:`6 <alm-24014__li368813032118>` to :ref:`7 <alm-24014__li153512414216>`. Then, check whether the alarm is automatically cleared one hour later.

   -  If yes, go to :ref:`9 <alm-24014__li127861713811>`.
   -  If no, go to :ref:`10 <alm-24014__li593632253716>`.

9. .. _alm-24014__li127861713811:

   Check whether this alarm is generated again during periodic system check.

   -  If yes, go to :ref:`10 <alm-24014__li593632253716>`.
   -  If no, no further action is required.

**Collect the fault information.**

10. .. _alm-24014__li593632253716:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Select **MonitorServer** in the required cluster for **Service**.

12. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767606.png
