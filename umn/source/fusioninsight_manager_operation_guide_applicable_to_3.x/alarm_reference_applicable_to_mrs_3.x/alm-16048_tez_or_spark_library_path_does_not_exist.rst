:original_name: ALM-16048.html

.. _ALM-16048:

ALM-16048 Tez or Spark Library Path Does Not Exist
==================================================

Description
-----------

The system checks the Tez and Spark library paths every 180 seconds. This alarm is generated when the Tez or Spark library path does not exist.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
16048    Major          Yes
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

The Hive on Tez and Hive on Spark functions are affected.

Possible Causes
---------------

The Tez or Spark library path is deleted from the HDFS.

Procedure
---------

**Check the default Hive data warehouse.**

#. Log in to the node where the client is located as user **root**.

#. Run the following command to check whether the **tezlib** or **sparklib** directory exists in the **hdfs://hacluster/user/{User name}/.Trash/Current/** director:

   **hdfs dfs -ls hdfs://hacluster/user/**\ *<username>*\ **/.Trash/Current/**

   For example, the following information shows that **/user/hive/tezlib/8.1.0.1/** and **/user/hive/sparklib/8.1.0.1/** exist.

   .. code-block::

      host01:/opt/client # hdfs dfs -ls hdfs://hacluster/user/test/.Trash/Current/
      Found 1 items
      drwx------   - test hadoop          0 2019-06-17 19:53 hdfs://hacluster/user/test/.Trash/Current/user

   -  If yes, go to :ref:`3 <alm-16048__li18824736175210>`.
   -  If no, go to :ref:`5 <alm-16048__li1182513369521>`.

#. .. _alm-16048__li18824736175210:

   Run the following command to restore **tezlib** and **sparklib**.

   **hdfs dfs -mv hdfs://hacluster/user/**\ *<username>*\ **/.Trash/Current/user/hive/tezlib/8.1.0.1/tez.tar.gz /user/hive/tezlib/8.1.0.1/tez.tar.gz**

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-16048__li1182513369521>`.

   **Collect fault information**.

#. .. _alm-16048__li1182513369521:

   Collect related information in the **.Trash/Current/** directory on the client background.

#. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None
