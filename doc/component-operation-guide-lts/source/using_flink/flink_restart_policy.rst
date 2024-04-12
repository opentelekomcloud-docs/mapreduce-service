:original_name: mrs_01_24779.html

.. _mrs_01_24779:

Flink Restart Policy
====================

Overview
--------

Flink supports different restart policies to control whether and how to restart a job when a fault occurs. If no restart policy is specified, the cluster uses the default restart policy. You can also specify a restart policy when submitting a job. For details about how to configure such a policy on the job development page of MRS 3.1.0 or later, see :ref:`Managing Jobs on the Flink Web UI <mrs_01_24024>`.

The restart policy can be specified by configuring the **restart-strategy** parameter in the Flink configuration file *Client installation directory*\ **/Flink/flink/conf/flink-conf.yaml** or can be dynamically specified in the application code. The configuration takes effect globally. Restart policies include **failure-rate** and the following two default policies:

-  **No restart**: If CheckPoint is not enabled, this policy is used by default.
-  **Fixed-delay**: If CheckPoint is enabled but no restart policy is configured, this policy is used by default.

No restart Policy
-----------------

When a fault occurs, the job fails and does not attempt to restart.

Configure the parameter as follows:

.. code-block::

   restart-strategy: none

fixed-delay Policy
------------------

When a fault occurs, the job attempts to restart for a fixed number of times. If the number of attempts exceeds the times you specified, the job fails. The restart policy waits for a fixed period of time between two consecutive restart attempts.

In the following example, a job fails if the job attempts to restart for three times at an interval of 10 seconds. Configure the parameters as follows:

.. code-block::

   restart-strategy: fixed-delay
   restart-strategy.fixed-delay.attempts: 3
   restart-strategy.fixed-delay.delay: 10 s

failure-rate Policy
-------------------

When a job fails, the job restarts directly. If the failure rate exceeds the value you configured, the job is considered as failed. The restart policy waits for a fixed period of time between two consecutive restart attempts.

In the following example, a job is considered as failed if the job attempts to restart for three times at an interval of 10 minutes. Configure the parameters as follows:

.. code-block::

   restart-strategy: failure-rate
   restart-strategy.failure-rate.max-failures-per-interval: 3
   restart-strategy.failure-rate.failure-rate-interval: 10 min
   restart-strategy.failure-rate.delay: 10 s

Choosing a Restart Policy
-------------------------

-  If you do not want to retry a failed job, select the **No restart** policy.

-  To retry a failed job, select the **failure-rate** policy. If the fixed-delay policy is used, the number of job failures may reach the maximum number of retries due to hardware faults such as network and memory faults. As a result, the job fails.

   To prevent repeated restarts when the failure-rate policy is used, configure parameters as follows:

   .. code-block::

      restart-strategy: failure-rate
      restart-strategy.failure-rate.max-failures-per-interval: 3
      restart-strategy.failure-rate.failure-rate-interval: 10 min
      restart-strategy.failure-rate.delay: 10 s
