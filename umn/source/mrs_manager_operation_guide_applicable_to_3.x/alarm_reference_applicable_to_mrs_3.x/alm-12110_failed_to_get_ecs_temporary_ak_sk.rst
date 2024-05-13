:original_name: ALM-12110.html

.. _ALM-12110:

ALM-12110 Failed to get ECS temporary AK/SK
===========================================

Description
-----------

The meta service periodically obtains the temporary AK/SK of the ECS. This alarm is generated when the meta service fails to obtain the temporary AK/SK.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12110    Major          Yes
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

In storage-compute decoupling scenarios, the cluster cannot obtain the latest temporary AK/SK, which may lead to failure access to OBS.

Possible Causes
---------------

-  The meta role of the MRS cluster is abnormal.
-  The cluster has been bound to an agency and accessed OBS but has been unbound from the agency. As a result, the cluster has not been bound to any agency.

Procedure
---------

**Check the status of the meta role.**

#. On MRS Manager of the cluster, choose **O&M** > **Alarm** > **Alarms**. On the page that is displayed, click |image1| in the row containing the alarm, and determine the IP address of the host for which the alarm is generated.

#. On MRS Manager of the cluster, choose **Cluster** > **Services** > **Meta**. On the page that is displayed, click the **Instance** tab, and check whether the meta role corresponding to the host for which the alarm is generated is normal.

   -  If yes, go to :ref:`4 <alm-12110__li1046594463117>`.
   -  If no, go to :ref:`3 <alm-12110__li183754571814>`.

#. .. _alm-12110__li183754571814:

   Select the abnormal role and choose **More** > **Restart Instance** to restart the abnormal meta role. After the restart is complete, check whether the alarm is cleared several minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-12110__li1046594463117>`.

**Rebind the cluster to an agency.**

4. .. _alm-12110__li1046594463117:

   Log in to the MRS management console.

5. In the navigation pane on the left, choose **Clusters** > **Active Clusters**. On the page that is displayed, click the cluster name to go to its overview page. Then, check whether the cluster is bound to an agency in the O&M management area.

   -  If yes, go to :ref:`7 <alm-12110__li546514420312>`.
   -  If no, go to :ref:`6 <alm-12110__li5465164415315>`.

6. .. _alm-12110__li5465164415315:

   Click **Manage Agency**. On the page that is displayed, rebind the cluster to an agency. Then check whether the alarm is cleared a few minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-12110__li546514420312>`.

7. .. _alm-12110__li546514420312:

   Contact O&M personnel.

.. |image1| image:: /_static/images/en-us_image_0000001582807757.png
