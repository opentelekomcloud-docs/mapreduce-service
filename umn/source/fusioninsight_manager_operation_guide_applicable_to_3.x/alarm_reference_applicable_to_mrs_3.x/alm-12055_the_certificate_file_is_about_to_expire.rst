:original_name: ALM-12055.html

.. _ALM-12055:

ALM-12055 The Certificate File Is About to Expire
=================================================

Description
-----------

The system checks the certificate file on 23:00 every day. This alarm is generated if the certificate file is about to expire within 30 days.

This alarm is cleared when a certificate that is not about to expire is imported and the alarm detection mechanism is triggered on the next hour.

.. note::

   For MRS 3.2.0-LTS.2 or later, the certificate file is checked at the beginning of each hour.

   For versions earlier than MRS 3.2.0-LTS.2, the certificate file is checked on 23:00 every day.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12055    Minor          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------+
| Name              | Meaning                                                           |
+===================+===================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated. |
+-------------------+-------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.           |
+-------------------+-------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.              |
+-------------------+-------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.                 |
+-------------------+-------------------------------------------------------------------+

Impact on the System
--------------------

Some functions are unavailable.

Possible Causes
---------------

The remaining validity period of a system certificate (CA certificate, HA root certificate, HA user certificate, Gaussdb root certificate, or Gaussdb user certificate) is less than 30 days.

Procedure
---------

**Check the alarm cause.**

#. On FusionInsight Manager, locate the target alarm in the real-time alarm list and click |image1|.

   View **Additional Information** to obtain the additional information about the alarm.

   -  If **CA Certificate** is displayed in the additional alarm information, log in to the active OMS management node as user **omm** and go to :ref:`2 <alm-12055__li31866665152950>`.
   -  If **HA root Certificate** is displayed in the additional information, view **Location** to obtain the name of the host involved in this alarm. Then, log in to the host as user **omm** and go to :ref:`3 <alm-12055__li35214520152950>`.
   -  If **HA server Certificate** is displayed in the additional information, view **Location** to obtain the name of the host involved in this alarm. Then, log in to the host as user **omm** and go to :ref:`4 <alm-12055__li089064874420>`.

**Check the validity period of the certificate files in the system.**

2. .. _alm-12055__li31866665152950:

   Check whether the remaining validity period of the CA certificate is smaller than the alarm threshold.

   Run the **bash ${CONTROLLER_HOME}/security/cert/conf/querycertvalidity.sh** command to check the effective time and due time of the CA root certificate.

   -  If yes, go to :ref:`5 <alm-12055__li12048984152950>`.
   -  If no, go to :ref:`7 <alm-12055__li48423894152950>`.

3. .. _alm-12055__li35214520152950:

   Check whether the remaining validity period of the HA root certificate is smaller than the alarm threshold.

   Run the **openssl x509 -noout -text -in ${CONTROLLER_HOME}/security/certHA/root-ca.crt** command to check the effective time and due time of the HA root certificate.

   -  If yes, go to :ref:`6 <alm-12055__li13690164035120>`.
   -  If no, go to :ref:`7 <alm-12055__li48423894152950>`.

4. .. _alm-12055__li089064874420:

   Check whether the remaining validity period of the HA user certificate is smaller than the alarm threshold.

   Run the **openssl x509 -noout -text -in ${CONTROLLER_HOME}/security/certHA/server.crt** command to check the effective time and due time of the HA user certificate.

   -  If yes, go to :ref:`6 <alm-12055__li13690164035120>`.
   -  If no, go to :ref:`7 <alm-12055__li48423894152950>`.

The following is an example of the effective time and due time of a CA or HA certificate:

.. code-block::

   Certificate:
       Data:
           Version: 3 (0x2)
           Serial Number:
               97:d5:0e:84:af:ec:34:d8
           Signature Algorithm: sha256WithRSAEncryption
           Issuer: C=CN, ST=xxx, L=yyy, O=zzz, OU=IT, CN=HADOOP.COM
           Validity
               Not Before: Dec 13 06:38:26 2016 GMT             // Effective time
               Not After : Dec 11 06:38:26 2026 GMT             // Due time

**Import certificate files.**

5. .. _alm-12055__li12048984152950:

   Import a new CA certificate file.

   Apply for or generate a new CA certificate file and import it to the system. Manually clear the alarm and check whether this alarm is generated again during periodic check.

   -  If yes, go to :ref:`7 <alm-12055__li48423894152950>`.
   -  If no, no further action is required.

6. .. _alm-12055__li13690164035120:

   Import a new HA certificate file.

   Apply for or generate a new HA certificate file and import it to the system. Manually clear the alarm and check whether this alarm is generated again during periodic check.

   -  If yes, go to :ref:`7 <alm-12055__li48423894152950>`.
   -  If no, no further action is required.

**Collect the fault information.**

7.  .. _alm-12055__li48423894152950:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  In the **Services** area, select **Controller**, **OmmServer**, **OmmCore**, and **Tomcat**, and click **OK**.

9.  Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448262.png
.. |image2| image:: /_static/images/en-us_image_0000001532927350.png
