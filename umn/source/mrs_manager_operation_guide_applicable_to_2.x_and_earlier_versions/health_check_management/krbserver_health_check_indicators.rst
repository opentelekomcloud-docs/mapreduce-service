:original_name: mrs_01_0289.html

.. _mrs_01_0289:

KrbServer Health Check Indicators
=================================

KerberosAdmin Service Availability
----------------------------------

**Indicator**: KerberosAdmin Service Availability

**Description**: The system checks the KerberosAdmin service status. If the check result is abnormal, the KerberosAdmin service is unavailable.

**Recovery Guide**: If the indicator check result is abnormal, the possible cause is that the node where the KerberosAdmin service is located is faulty or the SlapdServer service is unavailable. During the KerberosAdmin service recovery, try the following operations:

#. Check whether the node where the KerberosAdmin service locates is faulty.
#. Check whether the SlapdServer service is unavailable.

KerberosServer Service Availability
-----------------------------------

**Indicator**: KerberosServer Service Availability

**Description**: The system checks the KerberosServer service status. If the check result is abnormal, the KerberosServer service is unavailable.

**Recovery Guide**: If the indicator check result is abnormal, the possible cause is that the node where the KerberosServer service is located is faulty or the SlapdServer service is unavailable. During the KerberosServer service recovery, try the following operations:

#. Check whether the node where the KerberosServer service locates is faulty.
#. Check whether the SlapdServer service is unavailable.

Service Health Status
---------------------

**Indicator**: Service Status

**Description**: The system checks the KrbServer service status. If the check result is abnormal, the KrbServer service is unavailable.

**Recovery Guide**: If the indicator check result is abnormal, the possible cause is that the node where the KrbServer service resides is faulty or the LdapServer service is unavailable. For details, see the handling procedure of ALM-25500.

Alarm Check
-----------

**Indicator**: Alarm Information

**Description**: This indicator is used to check the alarm information about the KrbServer service. If any alarms exist, the KrbServer service may be abnormal.

**Recovery Guide**: If this indicator check result is abnormal, see the related alarm document to handle the alarms.
