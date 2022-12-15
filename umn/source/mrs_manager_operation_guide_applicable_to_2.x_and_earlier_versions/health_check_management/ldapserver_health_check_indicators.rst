:original_name: mrs_01_0291.html

.. _mrs_01_0291:

LdapServer Health Check Indicators
==================================

SlapdServer Service Availability
--------------------------------

**Indicator**: SlapdServer Service Availability

**Description**: The system checks the SlapdServer service status. If the status is abnormal, the SlapdServer service is unavailable.

**Recovery Guide**: If the indicator check result is abnormal, the possible cause is that the node where the SlapdServer service is located is faulty or the SlapdServer process is faulty. During the SlapdServer service recovery, try the following operations:

#. Check whether the node where the SlapdServer service locates is faulty. For details, see ALM-12006.
#. Check whether the SlapdServer process is normal. For details, see ALM-12007.

Service Health Status
---------------------

**Indicator**: Service Status

**Description**: This indicator is used to check the alarm information about the LdapServer service. If the status is abnormal, the LdapServer service is unavailable.

**Recovery Guide**: If the indicator check result is abnormal, the possible cause is that the node where the active LdapServer service resides is faulty or the active LdapServer process is faulty. For details, see ALM-25000.

Alarm Check
-----------

**Indicator**: Alarm Information

**Description**: This indicator is used to check the alarm information about the LdapServer service. If any alarms exist, the LdapServer service may be abnormal.

**Recovery Guide**: If this indicator check result is abnormal, see the related alarm document to handle the alarms.
