:original_name: alm_12055.html

.. _alm_12055:

ALM-12055 The Certificate File Is About to Expire
=================================================

Description
-----------

The system checks the certificate file on 23:00 every day. This alarm is generated if the certificate file is about to expire with a validity period less than days set in the alarm threshold.

This alarm is generated if the status of the newly imported certificate is valid.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12055    Minor          Yes
======== ============== ==========

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

The system reminds users that the license is about to expire. If the license expires, some functions are restricted and cannot be used properly.

Possible Causes
---------------

The remaining validity period of the CA certificate, HA root certificate, or HA user certificate is smaller than the alarm threshold.

Procedure
---------

**Check the alarm cause.**

#. Go to the MRS cluster details page and choose **Alarms**.

#. In the real-time alarm list, click the row that contains the alarm.

   In the **Alarm Details** area, view the additional information about the alarm.

   -  If **CA Certificate** is displayed in the additional alarm information, use PuTTY to log in to the active OMS management node as user **omm** and go to :ref:`3 <alm_12055__en-us_topic_0191813941_en-us_topic_0087039447_li31866665152950>`.
   -  If **HA root Certificate** is displayed in the additional information, check **Location** to obtain the name of the host involved in this alarm. Then use PuTTY to log in to the host as user **omm** and go to :ref:`4 <alm_12055__en-us_topic_0191813941_en-us_topic_0087039447_li35214520152950>`.
   -  If **HA server Certificate** is displayed in the additional information, check **Location** to obtain the name of the host involved in this alarm. Then use PuTTY to log in to the host as user **omm** and go to :ref:`5 <alm_12055__en-us_topic_0191813941_en-us_topic_0087039447_li289449152950>`.

**Check the validity period of the certificate files in the system.**

3. .. _alm_12055__en-us_topic_0191813941_en-us_topic_0087039447_li31866665152950:

   Check whether the remaining validity period of the CA certificate is smaller than the alarm threshold.

   Run the **openssl x509 -noout -text -in ${CONTROLLER_HOME}/security/cert/root/ca.crt** command to check the effective time and due time of the root certificate.

   -  If yes, go to :ref:`6 <alm_12055__en-us_topic_0191813941_en-us_topic_0087039447_li12048984152950>`.
   -  If no, go to :ref:`8 <alm_12055__en-us_topic_0191813941_li572522141314>`.

4. .. _alm_12055__en-us_topic_0191813941_en-us_topic_0087039447_li35214520152950:

   Check whether the remaining validity period of the HA root certificate is smaller than the alarm threshold.

   Run the **openssl x509 -noout -text -in ${CONTROLLER_HOME}/security/certHA/root-ca.crt** command to check the effective time and due time of the HA root certificate.

   -  If yes, go to :ref:`7 <alm_12055__en-us_topic_0191813941_en-us_topic_0087039447_li50119675152950>`.
   -  If no, go to :ref:`8 <alm_12055__en-us_topic_0191813941_li572522141314>`.

5. .. _alm_12055__en-us_topic_0191813941_en-us_topic_0087039447_li289449152950:

   Check whether the remaining validity period of the HA user certificate is smaller than the alarm threshold.

   Run the **openssl x509 -noout -text -in ${CONTROLLER_HOME}/security/certHA/server.crt** command to check the effective time and due time of the HA user certificate.

   -  If yes, go to :ref:`7 <alm_12055__en-us_topic_0191813941_en-us_topic_0087039447_li50119675152950>`.

   -  If no, go to :ref:`8 <alm_12055__en-us_topic_0191813941_li572522141314>`.

      The following is an example of the effective time and expiration time of a CA or HA certificate:

      .. code-block::

         Certificate:
             Data:
                 Version: 3 (0x2)
                 Serial Number:
                     97:d5:0e:84:af:ec:34:d8
                 Signature Algorithm: sha256WithRSAEncryption
                 Issuer: C=CountryName, ST=State, L=Locality, O=Organization, OU=IT, CN=HADOOP.COM
                 Validity
                     Not Before: Dec 13 06:38:26 2016 GMT             // Effective time
                     Not After : Dec 11 06:38:26 2026 GMT             // Expiration time

**Import certificate files.**

6. .. _alm_12055__en-us_topic_0191813941_en-us_topic_0087039447_li12048984152950:

   Import a new CA certificate file.

   Contact O&M personnel to apply for or generate a new CA certificate file and import it. Manually clear the alarm and check whether this alarm is generated again during periodic check.

   -  If yes, go to :ref:`8 <alm_12055__en-us_topic_0191813941_li572522141314>`.
   -  If no, no further action is required.

7. .. _alm_12055__en-us_topic_0191813941_en-us_topic_0087039447_li50119675152950:

   Import a new HA certificate file.

   Apply for or generate a new HA certificate file and import it by referring to :ref:`Replacing the HA Certificate <mrs_01_0571>`. Manually clear the alarm and check whether this alarm is generated again during periodic check.

   -  If yes, go to :ref:`8 <alm_12055__en-us_topic_0191813941_li572522141314>`.
   -  If no, no further action is required.

8. .. _alm_12055__en-us_topic_0191813941_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
