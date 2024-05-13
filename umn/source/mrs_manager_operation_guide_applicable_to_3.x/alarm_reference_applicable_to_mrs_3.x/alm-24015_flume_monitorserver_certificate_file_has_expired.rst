:original_name: ALM-24015.html

.. _ALM-24015:

ALM-24015 Flume MonitorServer Certificate File Has Expired
==========================================================

This section applies to MRS 3.2.0-LTS.2 or later.

Description
-----------

MonitorServer checks whether its certificate file in the system has expired every hour. This alarm is generated when the server certificate has expired. This alarm is automatically cleared when the MonitorServer certificate file becomes valid again.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24015    Major          Yes
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

The MonitorServer certificate file has expired.

Procedure
---------

**View alarm information.**

#. Log in to MRS Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing **ALM-24015 MonitorServer Certificate Has Expired**, and view the **Location** information. View the IP address of the instance for which the alarm is generated.

**Check whether the certificate file in the system is valid. If it is not, generate a new one.**

2. Log in to the node for which the alarm is generated as user **root** and run the **su - omm** command to switch to user **omm**.

3. Run the following command to go to the MonitorServer certificate file directory:

   **cd ${BIGDATA_HOME}/FusionInsight_Porter_*/install/FusionInsight-Flume-*/flume/conf**

4. Run the following command to check the effective time and expiration time of the user certificate to determine whether the certificate file is still in the validity period:

   **openssl x509 -noout -text -in ms_sChat.crt**

   -  If yes, go to :ref:`9 <alm-24015__li593632253716>`.
   -  If no, go to :ref:`5 <alm-24015__li160343112815>`.

5. .. _alm-24015__li160343112815:

   Run the following command to go to the Flume script directory:

   **cd ${BIGDATA_HOME}/FusionInsight_Porter_*/install/FusionInsight-Flume-*/flume/bin**

6. .. _alm-24015__li68486146283:

   Run the following command to generate a new certificate file. Then check whether the alarm is automatically cleared one hour later.

   **sh geneJKS.sh -m** *Custom password of the MonitorServer certificate on the server* **-n** *Custom password of the MonitorServer certificate on the client*

   -  If yes, go to :ref:`8 <alm-24015__li1788491915716>`.
   -  If no, go to :ref:`7 <alm-24015__li172496117507>`.

      .. note::

         The custom certificate passwords must meet the following complexity requirements:

         -  Contain at least four types of uppercase letters, lowercase letters, digits, and special characters.
         -  Contain 8 to 64 characters.
         -  Be changed periodically (for example, every three months), and certificates and trust lists are generated again to ensure security.

7. .. _alm-24015__li172496117507:

   Log in to the Flume node for which the alarm is generated as user **omm** and repeat :ref:`5 <alm-24015__li160343112815>` to :ref:`6 <alm-24015__li68486146283>`. Then, check whether the alarm is automatically cleared one hour later.

   -  If yes, go to :ref:`8 <alm-24015__li1788491915716>`.
   -  If no, go to :ref:`9 <alm-24015__li593632253716>`.

8. .. _alm-24015__li1788491915716:

   Check whether this alarm is generated again during periodic system check.

   -  If yes, go to :ref:`9 <alm-24015__li593632253716>`.
   -  If no, no further action is required.

**Collect the fault information.**

9.  .. _alm-24015__li593632253716:

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

.. |image1| image:: /_static/images/en-us_image_0000001532448470.png
