:original_name: en-us_topic_0000001152828323.html

.. _en-us_topic_0000001152828323:

How Do I Access Spark in a Cluster with Kerberos Authentication Enabled?
========================================================================

#. Log in to the master node in the cluster as user **root**.

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. If the Kerberos authentication is enabled for the current cluster, run the following command to authenticate the user.

   **kinit** *MRS cluster user*

   Example:

   If the development user is a machine-machine user, run **kinit -kt user.keytab sparkuser**.

   If the development user is a human-machine user, run **kinit sparkuser**.

#. Run the following command to connect to Spark Beeline:

   **spark-beeline**

#. Run commands on Spark Beeline. For example, create the table **test** in the **obs://mrs-word001/table/** directory.

   **create table test(id int) location 'obs://mrs-word001/table/';**

#. Run the following command to query all tables. If table **test** is displayed in the command output, OBS access is successful.

   **show tables;**

#. Press **Ctrl+C** to exit Spark Beeline.
