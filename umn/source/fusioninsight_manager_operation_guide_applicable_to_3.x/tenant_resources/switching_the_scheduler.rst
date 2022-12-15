:original_name: admin_guide_000133.html

.. _admin_guide_000133:

Switching the Scheduler
=======================

Scenario
--------

The newly installed MRS cluster uses the Superior scheduler by default. If the cluster is upgraded from an earlier version, you can switch the YARN scheduler from the Capacity scheduler to the Superior scheduler with a few clicks.

Prerequisites
-------------

-  The network connectivity of the cluster is proper and secure, and the YARN service status is normal.
-  During scheduler switching, tenants cannot be added, deleted, or modified. In addition, services cannot be started or stopped.

Impact on the System
--------------------

-  Because the ResourceManager is restarted during scheduler switching, submitting jobs to YARN will fail at that time.
-  During scheduler switching, tasks in a job being executed on YARN will continue, but new tasks cannot be started.
-  After scheduler switching is complete, jobs executed on YARN may fail, causing service interruptions.
-  After scheduler switching is complete, parameters of the Superior scheduler are used for tenant management.
-  After scheduler switching is complete, tenant queues whose capacity is 0 in the Capacity scheduler cannot be allocated resources in the Superior scheduler. As a result, jobs submitted to these tenant queues fail to be executed. Therefore, you are advised not to set the capacity of a tenant queue to 0 in the Capacity scheduler.
-  After scheduler switching is complete, you cannot add or delete resource pools, YARN node labels, or tenants during the observation period. If such an operation is performed, the scheduler cannot be rolled back to the Capacity scheduler.

   .. note::

      -  The recommended observation period for scheduler switching is one week. If resource pools, YARN node labels, or tenants are added or deleted during this period, the observation period ends immediately.

-  The scheduler rollback may cause the loss of partial or all YARN job information.

Switching from the Capacity Scheduler to the Superior Scheduler
---------------------------------------------------------------

#. Modify YARN service parameters and ensure that the YARN service status is normal.

   a. Log in to FusionInsight Manager as an administrator.

   b. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Yarn**. Click **Configurations** then **All Configurations**, search for **yarn.resourcemanager.webapp.pagination.enable**, and check whether the value is **true**.

      -  If yes, go to :ref:`1.c <admin_guide_000133__l62a2981fbee6466387b51feb634bb77f>`.
      -  If no, set the parameter to **true** and click **Save** to save the configuration. On the **Dashboard** tab page of YARN, choose **More** > **Restart Service**, verify the identity, and click **OK**. After the service is restarted, go to :ref:`1.c <admin_guide_000133__l62a2981fbee6466387b51feb634bb77f>`.

   c. .. _admin_guide_000133__l62a2981fbee6466387b51feb634bb77f:

      Choose **Cluster** > *Name of the desired cluster* > **Services**, and check whether the YARN service status is normal.

#. Log in to the active management node as user **omm**.

#. Switch the scheduler.

   The following switching modes are available:

   **0**: converts the Capacity scheduler configurations into the Superior scheduler configurations and then switches the Capacity scheduler to the Superior scheduler.

   **1**: converts the Capacity scheduler configurations into the Superior scheduler configurations only.

   **2**: switches the Capacity scheduler to the Superior scheduler only.

   -  Mode **0** is recommended if the cluster environment is simple and the number of tenants is less than 20.

      Run the following command:

      **sh ${BIGDATA_HOME}/om-server/om/sbin/switchScheduler.sh** **-c** *Cluster ID* **-m 0**

      .. note::

         You can choose **Cluster**, click the cluster name, and choose **Cluster Properties** on FusionInsight Manager to view the cluster ID.

      .. code-block::

         Start to convert Capacity scheduler to Superior Scheduler, clusterId=1
         Start to convert Capacity scheduler configurations to Superior. Please wait...
         Convert configurations successfully.
         Start to switch the Yarn scheduler to Superior. Please wait...
         Switch the Yarn scheduler to Superior successfully.

   -  If the cluster environment or tenant information is complex and you need to retain the queue configurations of the Capacity scheduler on the Superior scheduler, it is recommended that you use mode **1** first to convert the Capacity scheduler configurations, check the converted configurations, and then use mode **2** to switch the Capacity scheduler to the Superior scheduler.

      a. Run the following command to convert the Capacity scheduler configurations into the Superior scheduler configurations:

         **sh ${BIGDATA_HOME}/om-server/om/sbin/switchScheduler.sh -c** *Cluster ID* **-m 1**

         .. code-block::

            Start to convert Capacity scheduler to Superior Scheduler, clusterId=1
            Start to convert Capacity scheduler configurations to Superior. Please wait...
            Convert configurations successfully.

      b. Run the following command to switch the Capacity scheduler to the Superior scheduler:

         **sh ${BIGDATA_HOME}/om-server/om/sbin/switchScheduler.sh -c** *Cluster ID* **-m 2**

         .. code-block::

            Start to convert Capacity scheduler to Superior Scheduler, clusterId=1
            Start to switch the Yarn scheduler to Superior. Please wait...
            Switch the Yarn scheduler to Superior successfully.

   -  If you do not need to retain the queue configurations of the Capacity scheduler, use mode **2**.

      a. Log in to FusionInsight Manager and delete all tenants except the default tenant.

      b. On FusionInsight Manager, delete all resource pools except the default resource pool.

         Run the following command to switch the Capacity scheduler to the Superior scheduler:

         **sh ${BIGDATA_HOME}/om-server/om/sbin/switchScheduler.sh -c** *Cluster ID* **-m 2**

         .. code-block::

            Start to convert Capacity scheduler to Superior Scheduler, clusterId=1
            Start to switch the Yarn scheduler to Superior. Please wait...
            Switch the Yarn scheduler to Superior successfully.

   .. note::

      You can query the scheduler switching logs on the active management node.

      -  ${BIGDATA_LOG_HOME}/controller/aos/switch_scheduler.log
      -  ${BIGDATA_LOG_HOME}/controller/aos/aos.log
