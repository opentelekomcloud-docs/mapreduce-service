:original_name: admin_guide_000183.html

.. _admin_guide_000183:

Modifying the MRS Manager Routing Table
=======================================

Scenario
--------

When MRS Manager is installed, two pieces of routing information are automatically created on the active management node. You can run the **ip rule list** command to view the routing information, as shown in the following example:

.. code-block::

   0:from all lookup local
   32764:from all to 10.10.100.100 lookup ntp_rt   #NTP routing information created by MRS Manager (this information is unavailable if no external NTP clock source is configured).
   32765:from 192.168.0.117 lookup om_rt   #OM routing information created by the MRS Manager.
   32766:from all lookup main
   32767:from all lookup default

.. note::

   If no external NTP server has been configured, only the OM routing information will be created.

If the routing information created by MRS Manager conflicts with the routing information configured in the enterprise network planning, the cluster administrator can use **autoroute.sh** to disable or enable the routing information created by MRS Manager.

Impact on the System
--------------------

After the routing information created by MRS Manager is disabled and before the new routing information is set, MRS Manager cannot be accessed but the clusters are running properly.

Prerequisites
-------------

MRS Manager has been installed.

You have obtained routing information about the WS floating IP address.

Disable the Routing Information Created by the System
-----------------------------------------------------

#. Log in to the active management node as user **omm**. Run the following commands to disable the routing information created by the system:

   **cd ${BIGDATA_HOME}/om-server/om/sbin**

   **./autoroute.sh disable**

   .. code-block::

      Deactivating Route.
      Route operation (disable) successful.

#. Run the following command to view the execution result:

   **ip rule list**

   .. code-block::

      0:from all lookup local
      32766:from all lookup main
      32767:from all lookup default

#. Run the following command and enter the password of user **root** to switch to user **root**:

   **su - root**

#. Run the following commands to manually create the routing information about the WS floating IP address:

   **ip route add** *Network segment of the WS floating IP address/Subnet mask of the WS floating IP address* **scope link src** *WS floating IP address* **dev** *NIC of the WS floating IP address* **table om_rt**

   **ip route add default via** *Gateway of the WS floating IP address* **dev** *NIC of the WS floating IP address* **table om_rt**

   **ip rule add from** *WS floating IP address* **table om_rt**

   Example:

   **ip route add 192.168.0.0/255.255.255.0 scope link src 192.168.0.117 dev eth0:ws table om_rt**

   **ip route add default via 192.168.0.254 dev eth0:ws table om_rt**

   **ip rule add from 192.168.0.117 table om_rt**

   .. note::

      If IPv6 addresses are used, run the **ip -6 route add** command.

#. Run the following commands to manually create the NTP service routing information. Skip this step when no external NTP clock source is configured.

   **ip route add default via** *IP gateway of the NTP service* **dev** *NIC of the local IP address* **table ntp_rt**

   **ip rule add to** *ntpIP* **table ntp_rt**

   *NIC of the local IP address* indicates the NIC that can communicate with the network segment where the NTP server is located.

   Example:

   **ip route add default via 10.10.100.254 dev eth0 table ntp_rt**

   **ip rule add to 10.10.100.100 table ntp_rt**

#. View the execution result.

   In the following example, if the command output contains **om_rt** and **ntp_rt**, the operation is successful.

   **ip rule list**

   .. code-block::

      0:from all lookup local
      32764:from all to 10.10.100.100 lookup ntp_rt  #This information is not displayed if no external NTP clock source is configured.
      32765:from 192.168.0.117 lookup om_rt
      32766:from all lookup main
      32767:from all lookup default

Enable the Routing Information Created by the System
----------------------------------------------------

#. Log in to the active management node as user **omm**.

#. Run the following commands to enable the routing information created by the system:

   **cd ${BIGDATA_HOME}/om-server/om/sbin**

   **./autoroute.sh enable**

   .. code-block::

      Activating Route.
      Route operation (enable) successful.

#. View the execution result.

   In the following example, if the command output contains **om_rt** and **ntp_rt**, the operation is successful.

   **ip rule list**

   .. code-block::

      0:from all lookup local
      32764:from all to 10.10.100.100 lookup ntp_rt  #This information is not displayed if no external NTP clock source is configured.
      32765:from 192.168.0.117 lookup om_rt
      32766:from all lookup main
      32767:from all lookup default
