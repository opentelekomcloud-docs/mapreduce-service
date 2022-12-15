:original_name: mrs_01_0801.html

.. _mrs_01_0801:

Configuring ulimit for HBase and HDFS
=====================================

Symptom
-------

When you open an HDFS file, an error occurs due to the limit on the number of file handles. Information similar to the following is displayed.

.. code-block::

   IOException (Too many open files)

Procedure
---------

You can contact the system administrator to add file handles for each user. This is a configuration on the OS instead of HBase or HDFS. It is recommended that the system administrator configure the number of file handles based on the service traffic of HBase and HDFS and the rights of each user. If a user performs a large number of operations frequently on the HDFS that has large service traffic, set the number of file handles of this user to a large value.

#. Log in to the OSs of all nodes or clients in the cluster as user **root**, and go to the **/etc/security** directory.

#. Run the following command to edit the **limits.conf** file:

   **vi limits.conf**

   Add the following information to the file.

   .. code-block::

      hdfs  -       nofile  32768
      hbase -       nofile  32768

   **hdfs** and **hbase** indicate the usernames of the OSs that are used during the services.

   .. note::

      -  Only user **root** has the rights to edit the **limits.conf** file.
      -  If this modification does not take effect, check whether other nofile values exist in the **/etc/security/limits.d** directory. Such values may overwrite the values set in the **/etc/security/limits.conf** file.
      -  If a user needs to perform operations on HBase, set the number of file handles of this user to a value greater than **10000**. If a user needs to perform operations on HDFS, set the number of file handles of this user based on the service traffic. It is recommended that the value not be too small. If a user needs to perform operations on both HBase and HDFS, set the number of file handles of this user to a large value, such as **32768**.

#. Run the following command to check the limit on the number of file handles of a user:

   **su -** *user_name*

   **ulimit -n**

   The limit on the number of file handles of this user is displayed as follows.

   .. code-block::

      8194
