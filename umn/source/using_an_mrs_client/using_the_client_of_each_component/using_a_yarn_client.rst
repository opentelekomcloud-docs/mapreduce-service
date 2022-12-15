:original_name: mrs_01_24196.html

.. _mrs_01_24196:

Using a Yarn Client
===================

Scenario
--------

This section guides users to use a Yarn client in an O&M or service scenario.

Prerequisites
-------------

-  The client has been installed.

   For example, the installation directory is **/opt/hadoopclient**. The client directory in the following operations is only an example. Change it to the actual installation directory.

-  Service component users are created by the administrator as required. In security mode, machine-machine users need to download the keytab file. A human-machine user must change the password upon the first login. In common mode, you do not need to download the keytab file or change the password.

Using the Yarn Client
---------------------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory:

   **cd /opt/hadoopclient**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, run the following command to authenticate the user. In normal mode, user authentication is not required.

   **kinit** *Component service user*

#. Run the Yarn command. The following provides an example:

   **yarn application -list**

Client-related FAQs
-------------------

#. What Do I Do When the Yarn Client Exits Abnormally and Error Message "java.lang.OutOfMemoryError" Is Displayed After the Yarn Client Command Is Run?

   This problem occurs because the memory required for running the Yarn client exceeds the upper limit (128 MB by default) set on the Yarn client. For clusters of MRS 3.x or later: You can modify **CLIENT_GC_OPTS** in *<Client installation path>*\ **/HDFS/component_env** to change the memory upper limit of the Yarn client. For example, if you want to set the maximum memory to 1 GB, run the following command:

   .. code-block::

      export CLIENT_GC_OPTS="-Xmx1G"

   For clusters earlier than MRS 3.x: You can modify **GC_OPTS_YARN** in *< Client installation path >*\ **/HDFS/component_env** to change the memory upper limit of the Yarn client. For example, if you want to set the maximum memory to 1 GB, run the following command:

   .. code-block::

      export GC_OPTS_YARN="-Xmx1G"

   After the modification, run the following command to make the modification take effect:

   **source** <*Client installation path*>/**/bigdata_env**

#. How Can I Set the Log Level When the Yarn Client Is Running?

   By default, the logs generated during the running of the Yarn client are printed to the console. The default log level is INFO. To enable the DEBUG log level for fault locating, run the following command to export an environment variable:

   **export YARN_ROOT_LOGGER=DEBUG,console**

   Then run the Yarn Shell command to print DEBUG logs.

   If you want to print INFO logs again, run the following command:

   **export YARN_ROOT_LOGGER=INFO,console**
