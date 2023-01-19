:original_name: mrs_01_1753.html

.. _mrs_01_1753:

How Do I Delete UDFs on Multiple HiveServers at the Same Time?
==============================================================

Question
--------

How can I delete permanent user-defined functions (UDFs) on multiple HiveServers at the same time?

Answer
------

Multiple HiveServers share one MetaStore database. Therefore, there is a delay in the data synchronization between the MetaStore database and the HiveServer memory. If a permanent UDF is deleted from one HiveServer, the operation result cannot be synchronized to the other HiveServers promptly.

In this case, you need to log in to the Hive client to connect to each HiveServer and delete permanent UDFs on the HiveServers one by one. The operations are as follows:

#. Log in to the node where the Hive client is installed as the Hive client installation user.

#. Run the following command to go to the client installation directory:

   **cd** *Client installation directory*

   For example, if the client installation directory is **/opt/client**, run the following command:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to authenticate the user:

   **kinit** *Hive service user*

   .. note::

      The login user must have the Hive admin rights.

#. .. _mrs_01_1753__en-us_topic_0000001219029535_l7ef35cc9f4de4ef9966a1cda923d47e5:

   Run the following command to connect to the specified HiveServer:

   **beeline -u "jdbc:hive2://**\ *10.39.151.74*\ **:**\ *21066*\ **/default;sasl.qop=auth-conf;auth=KERBEROS;principal=**\ *hive*/*hadoop.<system domain name>@<system domain name>*"

   .. note::

      -  *10.39.151.74* is the IP address of the node where the HiveServer is located.
      -  *21066* is the port number of the HiveServer. The HiveServer port number ranges from 21066 to 21070 by default. Use the actual port number.
      -  *hive* is the username. For example, if the Hive1 instance is used, the username is **hive1**.
      -  You can log in to FusionInsight Manager, choose **System** > **Permission** > **Domain and Mutual Trust**, and view the value of **Local Domain**, which is the current system domain name.
      -  **hive/hadoop.\ *<system domain name>*** is the username. All letters in the system domain name contained in the username are lowercase letters.

#. Run the following command to enable the Hive admin rights:

   **set role admin;**

#. Run the following command to delete the permanent UDF:

   **drop function** *function_name*\ **;**

   .. note::

      -  *function_name* indicates the name of the permanent function.
      -  If the permanent UDF is created in Spark, the permanent UDF needs to be deleted from Spark and then from HiveServer by running the preceding command.

#. Check whether the permanent UDFs are deleted from all HiveServers.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <mrs_01_1753__en-us_topic_0000001219029535_l7ef35cc9f4de4ef9966a1cda923d47e5>`.
