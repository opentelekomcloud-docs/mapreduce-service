:original_name: admin_guide_000172.html

.. _admin_guide_000172:

Using a Client
==============

Scenario
--------

After the client is installed, you can use the shell command on the client in O&M or service scenarios, or use the sample project on the client during application development.

This section describes how to use the client in O&M scenario or service scenarios.

Prerequisites
-------------

-  You have installed the client.

   For example, the installation directory is **/opt/client**.

-  Service users of each component have been created by the system administrator based on service requirements.

   A machine-machine user needs to download the **keytab** file and a human-machine user needs to change the password upon the first login.

Procedure
---------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to switch to the client installation directory:

   **cd /opt/client**

#. Run the following command to set environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, authenticate the user. For a normal cluster, user authentication is not required.

   **kinit** *Component service user*

#. Run the **shell** command as required.
