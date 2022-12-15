:original_name: admin_guide_000284.html

.. _admin_guide_000284:

Encrypting the Communication Between the Controller and the Agent
=================================================================

Scenario
--------

After a cluster is installed, Controller and Agent need to communicate with each other. The Kerberos authentication is used during the communication. By default, the communication is not encrypted during the communication for the sake of cluster performance. Users who have demanding security requirements can use the method described in this section for encryption.

Impact on the System
--------------------

-  Controller and all Agents automatically restart, which interrupts FusionInsight Manager.
-  The performance of management nodes deteriorates in large clusters. You are advised to enable the encryption function for clusters with a maximum of 200 nodes.

Prerequisites
-------------

You have obtained the IP addresses of the active and standby management nodes.

Procedure
---------

#. Log in to the active management node as user **omm**.

#. Run the following command to disable logout upon timeout:

   **TMOUT=0**

   .. note::

      After the operations in this section are complete, run the **TMOUT=**\ *Timeout interval* command to restore the timeout interval in a timely manner. For example, **TMOUT=600** indicates that a user is logged out if the user does not perform any operation within 600 seconds.

#. Run the following command to go to the related directory:

   **cd ${CONTROLLER_HOME}/sbin**

#. Run the following command to enable communication encryption:

   **./enableRPCEncrypt.sh -t**

   Run the **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh** command to check whether **ResHAStatus** of the active management node Controller is **Normal** and whether you can log in to FusionInsight Manager again. If yes, the enablement is successful.

#. Run the following command to disable communication encryption when necessary:

   **./enableRPCEncrypt.sh -f**

   Run the **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh** command to check whether **ResHAStatus** of the active management node Controller is **Normal** and whether you can log in to FusionInsight Manager again. If yes, the enablement is successful.
