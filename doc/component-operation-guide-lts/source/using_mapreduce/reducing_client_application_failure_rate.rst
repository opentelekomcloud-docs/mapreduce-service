:original_name: mrs_01_0837.html

.. _mrs_01_0837:

Reducing Client Application Failure Rate
========================================

Scenario
--------

When the network is unstable or the cluster I/O and CPU are overloaded, client applications might encounter running failures.

Configuration
-------------

Adjust the following parameters in the **mapred-site.xml** configuration file on the client to reduce the client application failure rate:

.. note::

   The **mapred-site.xml** configuration file is in the **conf** directory of the client installation path, for example, **/opt/client/Yarn/config**.

.. table:: **Table 1** Parameter description

   +--------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                                  | Description                                                                                                                                                                                             | Default Value |
   +============================================+=========================================================================================================================================================================================================+===============+
   | mapreduce.reduce.shuffle.max-host-failures | Indicates the number of allowed failures of an MR task to read remote shuffle data in the Reduce process. When the number is set to be over 5, the client application failure rate can be reduced.      | 5             |
   +--------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | mapreduce.client.submit.file.replication   | Indicates the backup of job files on HDFS. MR tasks are dependent on the job files during running. When the number of backups is set to be over 10, the client application failure rate can be reduced. | 10            |
   +--------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
