:original_name: ALM-16045.html

.. _ALM-16045:

ALM-16045 Hive Data Warehouse Is Deleted
========================================

Description
-----------

The system checks the Hive data warehouse in every 60 seconds.This alarm is generated when the Hive data warehouse is deleted.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
16045    Critical       Yes
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

The default Hive data warehouse is deleted. As a result, creating databases or tables in the default data warehouse fails, and services are affected.

Possible Causes
---------------

Hive periodically checks the status of the default data warehouse and finds that the default data warehouse is deleted.

Procedure
---------

**Check the default Hive data warehouse.**

#. Log in to the node where the client is located as user **root**.

2. Run the following command to check whether the **warehouse** directory exists in **hdfs://hacluster/user/**\ *<username>*\ **/.Trash/Current/**.

   **hdfs dfs -ls** **hdfs://hacluster/user/**\ *<username>*\ **/.Trash/Current/**

   For example, if **user/hive/warehouse** exists:

   .. code-block::

      host01:/opt/client # hdfs dfs -ls hdfs://hacluster/user/test/.Trash/Current/
      Found 1 items
      drwx------   - test hadoop          0 2019-06-17 19:53 hdfs://hacluster/user/test/.Trash/Current/user

   -  If yes, go to :ref:`3 <alm-16045__li260541320316>`.
   -  If no, go to :ref:`5 <alm-16045__li185241657121312>`.

3. .. _alm-16045__li260541320316:

   By default, there is an automatic recovery mechanism for the data warehouse. You can wait for 5 ~10s to check whether the default data warehouse is restored. If the data warehouse is not recovered, manually run the following command to restore the data warehouse.

   **hdfs dfs -mv hdfs://hacluster/user/**\ *<username>*\ **/.Trash/Current/user/hive/warehouse /user/hive/warehouse**

4. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-16045__li185241657121312>`.

**Collect fault information**.

5. .. _alm-16045__li185241657121312:

   Collect related information in the **.Trash/Current/** directory on the client background.

6. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None
