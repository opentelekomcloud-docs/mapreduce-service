:original_name: mrs_08_00701.html

.. _mrs_08_00701:

ZooKeeper Basic Principle
=========================

ZooKeeper Overview
------------------

ZooKeeper is a distributed, highly available coordination service. ZooKeeper provides two functions:

-  Prevents the system from single point of failures (SPOFs) and provides reliable services for applications.
-  Provides distributed coordination services and manages configuration information.

ZooKeeper Architecture
----------------------

Nodes in a ZooKeeper cluster have three roles: Leader, Follower, and Observer. :ref:`Figure 1 <mrs_08_00701__f85514e7f75a34c4e9e1ad8c4b774f6d2>` shows the ZooKeeper architecture. Generally, an odd number (2N+1) of ZooKeeper servers are configured. At least (N+1) vote majority is required to successfully perform write operation.

.. _mrs_08_00701__f85514e7f75a34c4e9e1ad8c4b774f6d2:

.. figure:: /_static/images/en-us_image_0000001349310065.png
   :alt: **Figure 1** ZooKeeper architecture

   **Figure 1** ZooKeeper architecture

:ref:`Table 1 <mrs_08_00701__t2851557cbd1e4fadbbd7f2e21eb7b070>` describes the functions of each module shown in :ref:`Figure 1 <mrs_08_00701__f85514e7f75a34c4e9e1ad8c4b774f6d2>`.

.. _mrs_08_00701__t2851557cbd1e4fadbbd7f2e21eb7b070:

.. table:: **Table 1** ZooKeeper modules

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Module                            | Description                                                                                                                                                                                                                                                   |
   +===================================+===============================================================================================================================================================================================================================================================+
   | Leader                            | Only one node serves as the Leader in a ZooKeeper cluster. The Leader, elected by Followers using the ZooKeeper Atomic Broadcast (ZAB) protocol, receives and coordinates all write requests and synchronizes written information to Followers and Observers. |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Follower                          | Follower has two functions:                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                               |
   |                                   | -  Prevents SPOF. A new Leader is elected from Followers when the Leader is faulty.                                                                                                                                                                           |
   |                                   | -  Processes read requests and interacts with the Leader to process write requests.                                                                                                                                                                           |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Observer                          | The Observer does not take part in voting for election and write requests. It only processes read requests and forwards write requests to the Leader, increasing system processing efficiency.                                                                |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Client                            | Reads and writes data from or to the ZooKeeper cluster. For example, HBase can serve as a ZooKeeper client and use the arbitration function of the ZooKeeper cluster to control the active/standby status of the HMaster.                                     |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

If security services are enabled in the cluster, authentication is required during the connection to ZooKeeper. The authentication modes are as follows:

-  keytab mode: Obtain a human-machine user from the administrator for login to the platform and authentication, and obtain the keytab file of the user.
-  Ticket mode: Obtain a human-machine user from the administrator for subsequent secure login, enable the renewable and forwardable functions of the Kerberos service, set the ticket update interval, and restart Kerberos and related components.

   .. note::

      -  The default validity period of a user password is 90 days. Therefore, the validity period of the obtained keytab file is 90 days. To prolong the validity period of the keytab file, modify the user password policy and obtain the keytab file again. For details, see the *Administrator Guide*.
      -  The parameters for enabling the renewable and forwardable functions and setting the ticket update interval are on the **System** tab of the Kerberos service configuration page. The ticket update interval can be set to **kdc_renew_lifetime** or **kdc_max_renewable_life** based on the actual situation.

ZooKeeper Principle
-------------------

-  **Write Request**

   #. After the Follower or Observer receives a write request, the Follower or Observer sends the request to the Leader.
   #. The Leader coordinates Followers to determine whether to accept the write request by voting.
   #. If more than half of voters return a write success message, the Leader submits the write request and returns a success message. Otherwise, a failure message is returned.
   #. The Follower or Observer returns the processing results.

-  **Read Request**

   The client directly reads data from the Leader, Follower, or Observer.
