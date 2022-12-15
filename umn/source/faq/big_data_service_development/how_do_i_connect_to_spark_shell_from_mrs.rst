:original_name: mrs_03_1157.html

.. _mrs_03_1157:

How Do I Connect to Spark Shell from MRS?
=========================================

#. Log in to the Master node in the cluster as user **root**.

#. Run the following command to configure environment variables:

   **source** *Client installation directory*\ **/bigdata_env**

#. If Kerberos authentication is enabled for the cluster, authenticate the user. If Kerberos authentication is disabled, skip this step.

   Command: **kinit** *MRS cluster user*

   Example:

   -  If the user is a machine-machine user, run **kinit -kt user.keytab sparkuser**.
   -  If the user is a human-machine user, run **kinit sparkuser**.

#. Run the following command to connect to Spark shell:

   **spark-shell**
