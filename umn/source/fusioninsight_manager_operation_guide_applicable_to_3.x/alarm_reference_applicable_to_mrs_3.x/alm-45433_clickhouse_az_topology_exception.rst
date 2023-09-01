:original_name: ALM-45433.html

.. _ALM-45433:

ALM-45433 ClickHouse AZ Topology Exception
==========================================

Description
-----------

If the cross-AZ HA function is enabled for a cluster where ClickHouse has been deployed, the ClickHouse topology remains unchanged. This alarm is generated when the cross-AZ HA does not take effect if backup nodes of the same shard are in the same AZ.

This alarm is automatically cleared when the system detects that all shards meet the cross-AZ HA deployment requirements.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45433    Critical       Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The current deployment of the ClickHouse service does not support cross-AZ HA.

Possible Causes
---------------

After cross-AZ HA is enabled, all backup nodes of a shard are in the same AZ.

Procedure
---------

**Modify the AZ of backup nodes.**

#. Log in to the node where the client is installed as the client installation user. Run the following command to switch to the client installation directory:

   **cd** *{Client installation path}*

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to authenticate the user (skip this step in normal mode):

   **kinit** *Component service user*

#. Run the following command to log in to the client tool:

   **zkCli.sh -server**\ *Service IP address of the node where the ZooKeeper instance resides*\ **:**\ *Client port*

#. Run the following command to view the current topology:

   **get /clickhouse/topo**

   .. note::

      If the ClickHouse is installed with multiple services, run the **get /clickhouse{-n}/topo** command. For example, if the ClickHouse-1 is installed, run the **get /clickhouse-1/topo** command.

   .. code-block::

      [zk: 192.168.20.36:24002(CONNECTED) 0] get /clickhouse/topo

      <topo>
        <mcluster>
          <shard id="14" index="1">
            <server id="15">
              <replica>1</replica>
              <az>AZ1</az>
              <host>192-168-20-205</host>
              <port>21427</port>
            </server>
            <server id="16">
              <replica>2</replica>
              <az>AZ1</az>
              <host>192-168-20-2205</host>
              <port>21427</port>
            </server>
          </shard>
        </mcluster>
      </topo>

#. .. _alm-45433__li6955713123211:

   Select a host from the desired shard and deploy the host in another AZ.

#. Log in to FusionInsight Manager, click **Host**, select the host you have deployed in :ref:`6 <alm-45433__li6955713123211>` and choose **More** > **Reinstall** to reinstall the host.

#. Choose **Cluster** > **Cross-AZ HA**, click **Configure AZ and Policy** and change the AZ information of the reinstalled host to the AZ planned in the :ref:`6 <alm-45433__li6955713123211>`.

#. Wait for five minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-45433__li7445104417423>`.

**Collect fault information.**

10. .. _alm-45433__li7445104417423:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

11. Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **ClickHouseServer** for the target cluster.

12. Expand the **Hosts** list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

13. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927881.png
