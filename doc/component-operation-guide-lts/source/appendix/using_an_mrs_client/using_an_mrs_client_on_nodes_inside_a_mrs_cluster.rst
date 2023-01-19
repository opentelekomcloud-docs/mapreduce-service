:original_name: mrs_01_0788.html

.. _mrs_01_0788:

Using an MRS Client on Nodes Inside a MRS Cluster
=================================================

Scenario
--------

Before using the client, you need to install the client. For example, the installation directory is **/opt/hadoopclient**.

Procedure
---------

#. Log in to the Master node in the cluster as user **root**.

#. Run the **sudo su -** **omm** command to switch the current user.

#. Run the following command to go to the client directory:

   **cd /opt/hadoopclient**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user. If Kerberos authentication is disabled for the current cluster, skip this step:

   **kinit** *MRS cluster user*

   Example: **kinit admin**

   .. note::

      User **admin** is created by default for MRS clusters with Kerberos authentication enabled and is used for administrators to maintain the clusters.

#. Run the client command of a component directly.

   For example, run the **hdfs dfs -ls /** command to view files in the HDFS root directory.
