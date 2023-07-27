:original_name: ALM-45434.html

.. _ALM-45434:

ALM-45434 A Single Replica Exists in the ClickHouse Data Table
==============================================================

Description
-----------

This alarm is generated when a single replica is detected in a custom logical cluster after the custom logical cluster is enabled for ClickHouse.

This alarm is automatically cleared when the system detects that the custom logical cluster uses multiple replicas.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45434    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

If a hardware fault occurs, data cannot be restored.

Possible Causes
---------------

The **metrika.xml** file in the ClickHouse configuration directory contains single-replica configuration.

Procedure
---------

**Check whether the configuration in metrika.xml of the ClickHouse instance is correct.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm, and click |image1| to view the name of the host for which the alarm is generated. On the **Hosts** page, view the host IP address based on the host name.

#. Log in to the host where the ClickHouse instance is abnormal, go to the configuration directory of the ClickHouse instance, and run the following commands:

   **cd** ${BIGDATA_HOME}\ **/FusionInsight_ClickHouse\_**\ *Version*\ **/**\ x_x\ **\_ClickHouseServer/etc**

   **cat metrika.xml**

#. View the number of shards in each custom logical cluster and check that a single replica exists. Then, go to :ref:`4 <alm-45434__li153021955172417>`.

   .. note::

      If a shard contains only one node, a single replica exists in a logical cluster, as shown in the following:

      .. code-block::

         <shard>
           <internal_replication>true</internal_replication>
           <replica>
             <host>host-name1</host>
             <port>port</port>
             <user>clickhouse</user>
             <password/>
           </replica>
         </shard>

**Collect fault information.**

4. .. _alm-45434__li153021955172417:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

5. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

6. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

7. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087573.png
.. |image2| image:: /_static/images/en-us_image_0000001582927813.png
