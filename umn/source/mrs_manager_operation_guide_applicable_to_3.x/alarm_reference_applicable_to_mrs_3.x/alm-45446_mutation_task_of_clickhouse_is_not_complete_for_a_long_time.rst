:original_name: ALM-45446.html

.. _ALM-45446:

ALM-45446 Mutation Task of ClickHouse Is Not Complete for a Long Time
=====================================================================

.. note::

   This section is available for MRS 3.3.1-LTS or later version only.

Alarm Description
-----------------

The system checks mutation tasks every 5 minutes. This alarm is generated when the system detects that a mutation task has been running for at least **slow_mutation_cost_time** minutes. This alarm is automatically cleared when the system does not detect any running mutation task or the running time of a mutation task is less than **slow_mutation_cost_time** minutes.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
45446    Minor          Quality of service ClickHouse   Yes
======== ============== ================== ============ ============

Alarm Parameters
----------------

+----------------------+-------------+--------------------------------------------------------------------+
| Type                 | Parameter   | Description                                                        |
+======================+=============+====================================================================+
| Location Information | Source      | Specifies the cluster or system for which the alarm was generated. |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated.           |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

-  Server resources are occupied, and the performance of the ClickHouse service deteriorates.
-  Data is inconsistent.

Possible Causes
---------------

The data volume is too large. As a result, the mutation task runs slowly or is suspended.

Handling Procedure
------------------

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and view the role name and the IP address for the hostname in **Location**.

#. Log in to the node where the client is installed and run the following commands:

   **cd** *{Client installation path}*

   **source bigdata_env**

   -  Security mode (with Kerberos enabled):

      **kinit** *Component service user*

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--port** 21427 **--secure**

   -  Normal mode (with Kerberos disabled):

      **clickhouse client --host** *IP address of the ClickHouseServer instance for which the alarm is reported* **--user** *Username* **--password** **--port** 21423

#. .. _alm-45446__li1399613358:

   Log in to MRS Manager, choose **Cluster** > **Services** > **ClickHouse**, click **Configurations** and then **All Configurations**. Search for the value of the **slow_mutation_cost_time** parameter, enter the parameter value in the following SQL statement, and run the following statement to check whether any result is returned:

   **SELECT \* FROM system.mutations WHERE is_done = 0 AND create_time < now() - INTERVAL** *The value* **SECOND**

   .. note::

      Add the actual value of **slow_mutation_cost_time** to the preceding statement.

   -  If yes, go to :ref:`4 <alm-45446__li0271102163611>`.
   -  If no, go to :ref:`7 <alm-45446__li7516102842016>`.

#. .. _alm-45446__li0271102163611:

   Wait for a while and run the statement in :ref:`3 <alm-45446__li1399613358>` again. Check whether the value of **parts_to_do** in the returned result decreases.

   -  If yes, wait until the mutation task is complete.
   -  If no, go to :ref:`5 <alm-45446__li732219457436>`.

   |image1|

#. .. _alm-45446__li732219457436:

   If the value of **parts_to_do** remains unchanged, stop the mutation task. Run the following statement and run the statement in :ref:`3 <alm-45446__li1399613358>` again to check whether the current mutation task is in the returned result list:

   **KILL MUTATION WHERE database = '**\ *Database name*\ **' AND table = '**\ *Table name*\ **' AND mutation_id ='mutation ID'**

   -  If yes, go to :ref:`7 <alm-45446__li7516102842016>`.
   -  If no, go to :ref:`6 <alm-45446__li2535111318311>`.

   |image2|

6. .. _alm-45446__li2535111318311:

   Wait for several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-45446__li7516102842016>`.

**Collect fault information.**

7.  .. _alm-45446__li7516102842016:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

9.  Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002415261981.png
.. |image2| image:: /_static/images/en-us_image_0000002415342137.png
