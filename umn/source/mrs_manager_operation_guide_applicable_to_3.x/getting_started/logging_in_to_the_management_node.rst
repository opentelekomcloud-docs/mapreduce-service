:original_name: admin_guide_000005.html

.. _admin_guide_000005:

Logging In to the Management Node
=================================

Scenario
--------

Some O&M operation scripts and commands need to be run or can be run only on the active management node. You can identify and log in to the active or standby management node based on the following operations.

Checking and Logging In to the Active and Standby Management Nodes
------------------------------------------------------------------

#. Log in to MRS Manager.

#. Choose **System** > **OMS**.

   In the **Basic Information** area, **Current Active** indicates the host name of the active management node, and **Current Standby** indicates the host name of the standby management node.

   Click a host name to go to the host details page. On the host details page, record the IP address of the host.

#. Log in to the active or standby management node as user **root**.

Identifying the Active and Standby Management Nodes by Running Scripts and Logging In to Them
---------------------------------------------------------------------------------------------

#. Log in to any node where MRS Manager is installed as user **root**.

#. Run the following command to identify the active and standby management nodes:

   **su - omm**

   **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh**

   In the command output, the node whose **HAActive** is **active** is the active management node (Master1), and the node whose **HAActive** is **standby** is the standby node (Master2).

   .. code-block::

      HAMode
      double
      NodeName              HostName        HAVersion          StartTime                HAActive             HAAllResOK           HARunPhase
      192-168-0-30          Master1         V100R001C01        2021-09-01 07:12:05      active               normal               Actived
      192-168-0-24          Master2         V100R001C01        2021-09-01 07:14:02      standby              normal               Deactived

#. Run the following command to obtain the IP addresses of the active and standby management nodes:

   **cat /etc/hosts**

   Example IP addresses of the active and standby management nodes:

   .. code-block::

      127.0.0.1      localhost
      192.168.0.30    Master1
      192.168.0.24    Master2

#. Log in to the active or standby management node as user **root**.
