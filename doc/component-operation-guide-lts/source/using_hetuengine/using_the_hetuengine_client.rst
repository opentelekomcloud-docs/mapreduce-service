:original_name: mrs_01_1737.html

.. _mrs_01_1737:

Using the HetuEngine Client
===========================

Scenario
--------

If a compute instance is not created or started, you can log in to the HetuEngine client to create or start the compute instance. This section describes how to manage a compute instance on the client in the O&M or service scenario.

Prerequisites
-------------

-  The cluster client has been installed. For example, the installation directory is **/opt/client**.

-  You have created a common HetuEngine user, for example, **hetu_test** who has the permissions of the Hive (with Ranger disabled), **hetuuser**, and **default** queues.

   For details about how to create a user, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Procedure
---------

#. Log in to the node where the HetuEngine client resides as the user who installs the client, and switch to the client installation directory.

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Log in to the HetuEngine client based on the cluster authentication mode.

   -  In security mode, run the following command to complete user authentication and log in to the HetuEngine client:

      **kinit hetu_test**

      **hetu-cli --catalog hive --tenant default --schema default**

   -  In normal mode, run the following command to log in to the HetuEngine client:

      **hetu-cli --catalog hive --tenant default --schema default --user hetu_test**

      .. note::

         **hetu_test** is a service user who has at least the tenant role specified by **--tenant** and cannot be an OS user.

   Parameter description:

   -  **--catalog:** (Optional) Specifies the name of the specified data source.
   -  **--tenant**: (Optional) Specifies the tenant resource queue started by the cluster. Do not specify it as the default queue of a tenant. When this parameter is used, the service user must have the role permission of the tenant.
   -  **--schema**: (Optional) Specifies the name of the schema of the data source to be accessed.
   -  **--user**: (Mandatory in normal mode) Specifies the name of the user who logs in to the client to execute services. The user must have at least the role of the queue specified by **--tenant**.

   .. note::

      -  When you log in to the client for the first time, you need to start the HetuEngine cluster on the server. The client page is displayed 40 seconds later.
      -  The client supports SQL syntax and is compatible with the SQL syntax of the open-source openLooKeng 1.2.0.
