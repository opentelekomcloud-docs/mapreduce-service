:original_name: ALM-12102.html

.. _ALM-12102:

ALM-12102 AZ HA Component Is Not Deployed Based on DR Requirements
==================================================================

Description
-----------

The alarm module checks the deployment status of AZ HA components every 5 minutes. This alarm is generated when the components that support DR are not deployed based on DR requirements after AZ is enabled. This alarm is cleared when the components are deployed based on DR requirements.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12102    Major          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The cross-AZ HA capability of a single cluster is affected.

Possible Causes
---------------

The roles of the components that support DR are not deployed based on DR requirements.

Procedure
---------

**Obtain alarm information.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**.
#. In the alarm list, click |image1| in the row that contains the alarm and view the roles that are not deployed based on DR requirements in **Additional Information**.

**Redeploy the role instance.**

3. Choose **Cluster** > **Services** > *Name of the desired service* > **Instance**. On the instance page, redeploy or adjust the role instance.
4. Check whether the alarm is cleared 10 minutes later.

   -  If yes, no further action is required.
   -  If no, contact O&M personnel.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127297.png
