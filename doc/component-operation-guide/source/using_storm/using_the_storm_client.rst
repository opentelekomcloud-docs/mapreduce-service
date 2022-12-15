:original_name: mrs_01_2065.html

.. _mrs_01_2065:

Using the Storm Client
======================

Scenario
--------

This section describes how to use the Storm client in an O&M scenario or service scenario.

Prerequisites
-------------

-  You have installed the client. For example, the installation directory is **/opt/hadoopclient**.
-  Service component users are created by the administrator as required. In security mode, machine-machine users have downloaded the keytab file. A human-machine user must change the password upon the first login. (Not involved in normal mode)

Procedure
---------

#. Prepare the client based on service requirements. Log in to the node where the client is installed.

   Log in to the node where the client is installed.

#. Run the following command to go to the client installation directory:

   **cd /opt/hadoopclient**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If multiple Storm instances are installed, run the following command to load the environment variables of a specific instance when running the Storm command to submit the topology. Otherwise, skip this step. The following command uses the instance Storm-2 as an example.

   **source Storm-2/component_env**

#. Run the following command to perform user authentication (skip this step in normal mode):

   **kinit** *Component service user*

#. Run the following command to perform operations on the client:

   For example, run the following command:

   -  **cql**
   -  **storm**

   .. note::

      A Storm client cannot be connected to secure and non-secure ZooKeepers at the same time.
