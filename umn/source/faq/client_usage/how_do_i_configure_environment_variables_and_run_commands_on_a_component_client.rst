:original_name: mrs_03_1031.html

.. _mrs_03_1031:

How Do I Configure Environment Variables and Run Commands on a Component Client?
================================================================================

#. Log in to any Master node as user **root**.

#. Run the **su - omm** command to switch to user **omm**.

#. Run the **cd** *Client installation directory* command to switch to the client.

#. Run the **source bigdata_env** command to configure environment variables.

   If Kerberos authentication is enabled for the current cluster, run the **kinit** *Component service user* command to authenticate the user. If Kerberos authentication is disabled, skip this step.

#. After the environment variables are configured, run the client command of the component. For example, to view component information, you can run the HDFS client command **hdfs dfs -ls /** to view the HDFS root directory file.
