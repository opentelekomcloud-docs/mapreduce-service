:original_name: mrs_01_1750.html

.. _mrs_01_1750:

Switching the Hive Execution Engine to Tez
==========================================

Scenario
--------

Hive can use the Tez engine to process data computing tasks. Before executing a task, you can manually switch the execution engine to Tez.

Prerequisites
-------------

The TimelineServer role of the Yarn service has been installed in the cluster and is running properly.

Switching the Execution Engine on the Client to Tez
---------------------------------------------------

#. Install and log in to the Hive client. For details, see :ref:`Using a Hive Client <mrs_01_0952>`.

#. Run the following commands for MRS 3.1.2 to switch the engine and enable the **yarn.timeline-service.enabled** parameter:

   **set hive.execution.engine=tez**;

   **set yarn.timeline-service.enabled=true**;

   .. note::

      -  After **yarn.timeline-service.enabled** is enabled, you can view the details about the tasks executed by the Tez engine on TezUI. After this function is enabled, task information will be reported to TimelineServer. If the TimelineServer instance is faulty, the task will fail.
      -  Tez uses the ApplicationMaster buffer pool. Therefore, **yarn.timeline-service.enabled** must be enabled before Tez tasks are submitted. Otherwise, this parameter cannot take effect and you need to log in to the client again to configure it.
      -  When the execution engine needs to be switched to another engine, you need to run the **set yarn.timeline-service.enabled=false** command on the client to disable the **yarn.timeline-service.enabled** parameter.
      -  To specify a Yarn running queue, run the **set tez.queue.name=default** command on the client.

#. For MRS 3.2.0 and later versions, run the following command to switch the engine:

   **set hive.execution.engine=tez**;

   .. note::

      To specify a running Yarn queue, run the **set tez.queue.name=default** command on the client.

#. Submit and execute the Tez tasks.

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Tez** > **TezUI**\ *(host name)* to view the task execution status on the TezUI page.

Switching the Default Execution Engine of Hive to Tez
-----------------------------------------------------

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Configurations** > **All Configurations** > **HiveServer(Role)**, and search for **hive.execution.engine**.
#. Set **hive.execution.engine** to **tez**.
#. Choose **Hive(Service)** > **Customization** and search for **yarn.site.customized.configs**\  for MRS 3.1.2.
#. Add a customized parameter **yarn.timeline-service.enabled** next to **yarn.site.customized.configs** and set its value to **true**\ for MRS 3.1.2.

   .. note::

      -  After **yarn.timeline-service.enabled** is enabled, you can view the details about the tasks executed by the Tez engine on TezUI. After this function is enabled, task information will be reported to TimelineServer. If the TimelineServer instance is faulty, the task will fail.
      -  Tez uses the ApplicationMaster buffer pool. Therefore, **yarn.timeline-service.enabled** must be enabled before Tez tasks are submitted. Otherwise, this parameter cannot take effect and you need to log in to the client again to configure it.
      -  When the execution engine needs to be switched to another one, you need to set the value of parameter **yarn.timeline-service.enabled** to **false**.

#. Click **Save**. In the displayed confirmation dialog box, click **OK**.
#. Choose **Dashboard** > **More** > **Restart Service** to restart the Hive service. Enter the password to restart the service.
#. Install and log in to the Hive client. For details, see :ref:`Using a Hive Client <mrs_01_0952>`.
#. Submit and execute the Tez tasks.
#. Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services** > **Tez** > **TezUI**\ *(host name)*. On the displayed TezUI page, view the task execution status.
