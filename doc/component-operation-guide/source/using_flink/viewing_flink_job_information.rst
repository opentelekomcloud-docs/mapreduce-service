:original_name: mrs_01_0784.html

.. _mrs_01_0784:

Viewing Flink Job Information
=============================

You can view Flink job information on the Yarn web UI.

Prerequisites
-------------

The Flink service has been installed in a cluster.

Accessing the Yarn Web UI
-------------------------

#. Go to the Yarn service page.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services** > **Yarn** > **Yarn Summary**.
   -  For MRS 1.9.2 or later, click the cluster name on the MRS console and choose **Components** > **Yarn** > **Yarn Summary**.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   -  For MRS 3.\ *x* or later, log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **Instance** > **Dashboard**.

#. Click the link next to **ResourceManager WebUI** to go to the Yarn web UI page.
