:original_name: mrs_01_1980.html

.. _mrs_01_1980:

Using the external shuffle service to improve performance
=========================================================

Scenario
--------

When the Spark system runs applications that contain a shuffle process, an executor process also writes shuffle data and provides shuffle data for other executors in addition to running tasks. If the executor is heavily loaded and GC is triggered, the executor cannot provide shuffle data for other executors, affecting task running.

The external shuffle service is an auxiliary service in NodeManager. It captures shuffle data to reduce the load on executors. If GC occurs on an executor, tasks on other executors are not affected.

Procedure
---------

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Spark2x** > **Configurations**. Select **All Configurations**.
#. Choose **SparkResource2x** > **Default** and modify the following parameters.

   .. table:: **Table 1** Parameter list

      ============================= ============= ==========
      Parameter                     Default Value Changed To
      ============================= ============= ==========
      spark.shuffle.service.enabled false         true
      ============================= ============= ==========

#. Restart the Spark2x service for the configuration to take effect.

   .. note::

      To use the External Shuffle Service function on the Spark2x client, you need to download and install the Spark2x client again.
