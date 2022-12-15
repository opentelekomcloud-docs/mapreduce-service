:original_name: alm_12054.html

.. _alm_12054:

ALM-12054 The Certificate File Is Invalid
=========================================

Description
-----------

The system checks whether the certificate file is invalid (has expired or is not yet valid) on 23:00 every day. This alarm is generated when the certificate file is invalid.

This alarm is cleared when the status of the newly imported certificate is valid.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12054    Major          Yes
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

The system reminds users that the certificate file is invalid. If the certificate file is invalid, some functions are restricted and cannot be used properly.

Possible Causes
---------------

No certificate (HA root certificate or HA user certificate) is imported to the system, the certificate fails to be imported, or the certificate file is invalid.

Procedure
---------

**Check the alarm cause.**

#. Go to the MRS cluster details page and choose **Alarms**.

#. In the real-time alarm list, click the row that contains the alarm.

   In the **Alarm Details** area, view the additional information about the alarm.

   -  If **CA Certificate** is displayed in the additional alarm information, use PuTTY to log in to the active OMS management node as user **omm** and go to :ref:`3 <alm_12054__en-us_topic_0191813937_en-us_topic_0087039414_li2768003415237>`.
   -  If **HA root Certificate** is displayed in the additional information, check **Location** to obtain the name of the host involved in this alarm. Then use PuTTY to log in to the host as user **omm** and go to :ref:`4 <alm_12054__en-us_topic_0191813937_en-us_topic_0087039414_li6628516015237>`.
   -  If **HA server Certificate** is displayed in the additional information, check **Location** to obtain the name of the host involved in this alarm. Then use PuTTY to log in to the host as user **omm** and go to :ref:`5 <alm_12054__en-us_topic_0191813937_en-us_topic_0087039414_li3401162015237>`.

**Check the validity period of the certificate files in the system.**

3. .. _alm_12054__en-us_topic_0191813937_en-us_topic_0087039414_li2768003415237:

   Check whether the current system time is in the validity period of the CA certificate.

   Run the **openssl x509 -noout -text -in ${CONTROLLER_HOME}/security/cert/root/ca.crt** command to check the effective time and due time of the root certificate.

   -  If yes, go to :ref:`8 <alm_12054__en-us_topic_0191813937_li572522141314>`.
   -  If no, go to :ref:`6 <alm_12054__en-us_topic_0191813937_en-us_topic_0087039414_li99782015237>`.

4. .. _alm_12054__en-us_topic_0191813937_en-us_topic_0087039414_li6628516015237:

   Check whether the current system time is in the validity period of the HA root certificate.

   Run the **openssl x509 -noout -text -in ${CONTROLLER_HOME}/security/certHA/root-ca.crt** command to check the effective time and due time of the HA root certificate.

   -  If yes, go to :ref:`8 <alm_12054__en-us_topic_0191813937_li572522141314>`.
   -  If no, go to :ref:`7 <alm_12054__en-us_topic_0191813937_en-us_topic_0087039414_li3092985115237>`.

5. .. _alm_12054__en-us_topic_0191813937_en-us_topic_0087039414_li3401162015237:

   Check whether the current system time is in the validity period of the HA user certificate.

   Run the **openssl x509 -noout -text -in ${CONTROLLER_HOME}/security/certHA/server.crt** command to check the effective time and due time of the HA user certificate.

   -  If yes, go to :ref:`8 <alm_12054__en-us_topic_0191813937_li572522141314>`.

   -  If no, go to :ref:`7 <alm_12054__en-us_topic_0191813937_en-us_topic_0087039414_li3092985115237>`.

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

6. .. _alm_12054__en-us_topic_0191813937_en-us_topic_0087039414_li99782015237:

   Import a new CA certificate file.

   Contact O&M personnel to apply for or generate a new CA certificate file and import it. Manually clear the alarm and check whether this alarm is generated again during periodic check.

   -  If yes, go to :ref:`8 <alm_12054__en-us_topic_0191813937_li572522141314>`.
   -  If no, no further action is required.

7. .. _alm_12054__en-us_topic_0191813937_en-us_topic_0087039414_li3092985115237:

   Import a new HA certificate file.

   Apply for or generate a new HA certificate file and import it by referring to :ref:`Replacing the HA Certificate <mrs_01_0571>`. Manually clear the alarm and check whether this alarm is generated again during periodic check.

   -  If yes, go to :ref:`8 <alm_12054__en-us_topic_0191813937_li572522141314>`.
   -  If no, no further action is required.

8. .. _alm_12054__en-us_topic_0191813937_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
