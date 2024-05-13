:original_name: ALM-16046.html

.. _ALM-16046:

ALM-16046 Hive Data Warehouse Permission Is Modified
====================================================

Description
-----------

The system checks the Hive data warehouse permission in every 60 seconds. This alarm is generated if the permission is modified.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
16046    Critical       Yes
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

If the permission on the Hive default data warehouse is modified, the permission for users or user groups to create databases or tables in the default data warehouse is changed.

Possible Causes
---------------

Hive periodically checks the status of the default data warehouse and finds that default data warehouse permission is changed.

Procedure
---------

**Check the Hive default data warehouse permission.**

#. Log in to the node where the client is located as user **root**.

2. Run the following command to go to the HDFS client installation directory:

   **cd** *Client installation directory*

   **source bigdata_env**

   **kinit** *User who has the supergroup permission* (Skip this step for a common cluster.)

3. Run the following command to restore the default data warehouse permission:

   -  Security mode: **hdfs dfs -chmod 770 hdfs://hacluster/user/hive/warehouse**
   -  Non-security mode: **hdfs dfs -chmod 777 hdfs://hacluster/user/hive/warehouse**

4. Check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`5 <alm-16046__li14150557160>`.

**Collect fault information**.

5. .. _alm-16046__li14150557160:

   Collect related information in the **hdfs://hacluster/user/hive/warehouse** directory on the client background.

6. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None
