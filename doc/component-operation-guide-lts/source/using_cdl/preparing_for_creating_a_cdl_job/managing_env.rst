:original_name: mrs_01_24255.html

.. _mrs_01_24255:

Managing ENV
============

Scenario
--------

To capture data to or from Hudi, create and manage Hudi environment variables by performing the operations in this section.

Prerequisites
-------------

A user with the CDL management permission has been created for the cluster with Kerberos authentication enabled.

Procedure
---------

#. Access the CDLService web UI as a user with the CDL management permissions or the **admin** user (for the cluster where Kerberos authentication is not enabled). For details, see :ref:`Logging In to the CDLService WebUI <mrs_01_24236>`.

#. Choose **ENV Management** and click **Add Env**. In the displayed dialog box, set related parameters.

   .. table:: **Table 1** Parameters for adding an ENV

      +------------------+------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter        | Description                                                                                                | Example Value |
      +==================+============================================================================================================+===============+
      | Name             | ENV name                                                                                                   | spark-env     |
      +------------------+------------------------------------------------------------------------------------------------------------+---------------+
      | Type             | ENV type                                                                                                   | spark         |
      +------------------+------------------------------------------------------------------------------------------------------------+---------------+
      | Driver Memory    | Memory for the driver process, in GB ( by default).                                                        | 1 GB          |
      +------------------+------------------------------------------------------------------------------------------------------------+---------------+
      | Executor Memory  | Memory size for each Executor process, in GB by default. Its string format is the same as that of JVM.     | 1 GB          |
      +------------------+------------------------------------------------------------------------------------------------------------+---------------+
      | Executor Cores   | Number of CPU cores occupied by each Executor                                                              | 1             |
      +------------------+------------------------------------------------------------------------------------------------------------+---------------+
      | Number Executors | Number of Executors                                                                                        | 1             |
      +------------------+------------------------------------------------------------------------------------------------------------+---------------+
      | Queue            | Name of the Yarn tenant queue. Jobs are submitted to the default queue if this parameter is not specified. | ``-``         |
      +------------------+------------------------------------------------------------------------------------------------------------+---------------+
      | Description      | ENV description                                                                                            | ``-``         |
      +------------------+------------------------------------------------------------------------------------------------------------+---------------+

#. Click **OK**.

   After the ENV is created, you can click **Edit** or **Delete** in the **Operation** column to edit or delete the ENV, respectively.
