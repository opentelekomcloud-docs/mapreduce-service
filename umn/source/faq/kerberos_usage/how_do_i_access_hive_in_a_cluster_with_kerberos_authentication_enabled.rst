:original_name: mrs_03_1152.html

.. _mrs_03_1152:

How Do I Access Hive in a Cluster with Kerberos Authentication Enabled?
=======================================================================

#. Log in to the master node in the cluster as user **root**.

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user:

   **kinit** *MRS cluster user*

   Example: **kinit hiveuser**

   The current user must have the permission to create Hive tables..

#. Run the client command of the Hive component.

   **beeline**

#. Run the Hive command in Beeline, for example:

   **create table test_obs(a int, b string) row format delimited fields terminated by "," stored as textfile location "obs://test_obs";**

#. Press **Ctrl+C** to exit the Hive Beeline.
