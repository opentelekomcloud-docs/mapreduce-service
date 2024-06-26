:original_name: ALM-24013.html

.. _ALM-24013:

ALM-24013 Flume MonitorServer Certificate File Is Invalid or Damaged
====================================================================

This section applies to MRS 3.2.0-LTS.2 or later.

Description
-----------

MonitorServer checks whether its certificate file is valid (whether the certificate exists and whether the certificate format is correct) every hour. This alarm is generated when the certificate file is invalid or damaged. This alarm is automatically cleared when the certificate file becomes valid again.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24013    Major          Yes
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

The Flume client cannot access the Flume server.

Possible Causes
---------------

The MonitorServer certificate file is invalid or damaged.

Procedure
---------

**View alarm information.**

#. Log in to MRS Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing **ALM-24013 MonitorServer Certificate File Is Invalid or Damaged**, and view the **Location** information. View the IP address of the instance for which the alarm is generated.

**Check whether the certificate file in the system is valid. If it is not, generate a new one.**

2. Log in to the node for which the alarm is generated as user **root** and run the **su - omm** command to switch to user **omm**.

3. Run the following command to go to the MonitorServer certificate file directory:

   **cd ${BIGDATA_HOME}/FusionInsight_Porter_*/install/FusionInsight-Flume-*/flume/conf**

4. Run the **ls -l** command to check whether the **ms_sChat.crt** file exists:

   -  If yes, go to :ref:`5 <alm-24013__li224142155111>`.
   -  If no, go to :ref:`6 <alm-24013__li20454978185>`.

5. .. _alm-24013__li224142155111:

   Run the **openssl x509 -in ms_sChat.crt -text -noout** command to check whether certificate details are displayed.

   -  If yes, go to :ref:`9 <alm-24013__li593632253716>`.
   -  If no, go to :ref:`6 <alm-24013__li20454978185>`.

6. .. _alm-24013__li20454978185:

   Run the following command to go to the Flume script directory:

   **cd ${BIGDATA_HOME}/FusionInsight_Porter_*/install/FusionInsight-Flume-*/flume/bin**

7. Run the following command to generate a new certificate file. Then check whether the alarm is automatically cleared one hour later.

   **sh geneJKS.sh -m** *Custom password of the MonitorServer certificate on the server* **-n** *Custom password of the MonitorServer certificate on the client*

   -  If yes, go to :ref:`8 <alm-24013__li57811511185514>`.
   -  If no, go to :ref:`9 <alm-24013__li593632253716>`.

      .. note::

         The custom certificate passwords must meet the following complexity requirements:

         -  Contain at least four types of uppercase letters, lowercase letters, digits, and special characters.
         -  Contain 8 to 64 characters.
         -  Be changed periodically (for example, every three months), and certificates and trust lists are generated again to ensure security.

8. .. _alm-24013__li57811511185514:

   Check whether this alarm is generated again during periodic system check.

   -  If yes, go to :ref:`9 <alm-24013__li593632253716>`.
   -  If no, no further action is required.

**Collect the fault information.**

9.  .. _alm-24013__li593632253716:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Select **MonitorServer** in the required cluster for **Service**.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087565.png
