:original_name: mrs_01_2095.html

.. _mrs_01_2095:

Using a ZooKeeper Client
========================

Scenario
--------

Use a ZooKeeper client in an O&M scenario or service scenario.

Prerequisites
-------------

You have installed the client. For example, the installation directory is **/opt/client**. The client directory in the following operations is only an example. Change it based on the actual installation directory onsite.

Procedure
---------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to authenticate the user: (skip this step in common mode):

   **kinit** *Component service user*

#. Run the following command to log in to the client tool:

   **zkCli.sh -server** *service IP address of the node where the ZooKeeper role instance locates*\ **:**\ *client port*
