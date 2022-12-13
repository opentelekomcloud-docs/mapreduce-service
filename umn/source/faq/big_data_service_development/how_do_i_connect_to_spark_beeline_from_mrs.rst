:original_name: mrs_03_1158.html

.. _mrs_03_1158:

How Do I Connect to Spark Beeline from MRS?
===========================================

#. Log in to the master node in the cluster as user **root**.

#. Run the following command to configure environment variables:

   **source** *Client installation directory*\ **/bigdata_env**

#. If Kerberos authentication is enabled for the cluster, authenticate the user. If Kerberos authentication is disabled, skip this step.

   Command: **kinit** *MRS cluster user*

   Example:

   -  If the user is a machine-machine user, run **kinit -kt user.keytab sparkuser**.
   -  If the user is a human-machine user, run **kinit sparkuser**.

#. Run the following command to connect to Spark Beeline:

   **spark-beeline**

#. Run commands on Spark Beeline. For example, create the table **test** in the **obs://mrs-word001/table/** directory.

   **create table test(id int) location 'obs://mrs-word001/table/';**

#. Query all tables.

   **show tables;**

   If the table **test** is displayed in the command output, OBS is successfully accessed.


   .. figure:: /_static/images/en-us_image_0264281176.png
      :alt: **Figure 1** Returned table name

      **Figure 1** Returned table name

#. Press **Ctrl+C** to exit the Spark Beeline.
