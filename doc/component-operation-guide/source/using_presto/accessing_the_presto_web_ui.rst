:original_name: mrs_01_0433.html

.. _mrs_01_0433:

Accessing the Presto Web UI
===========================

You can view the Presto statistics on the graphical Presto web UI. You are advised to use Google Chrome to access the Presto web UI because it cannot be accessed using Internet Explorer.

Prerequisites
-------------

-  Presto has been installed in a cluster.
-  The cluster client has been installed, for example, in the **/opt/client** directory. The client directory in the following operations is only an example. Change it based on the actual installation directory onsite.


Accessing the Presto Web UI
---------------------------

-  Method 1 (for MRS 3.\ *x* or later)

   #. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. Choose **Cluster** > *Name of the target cluster* > **Services**.
   #. Select **Presto**. In the **Basic Information** area, click **Coordinator(Coordinator)** next to **Coordinator WebUI**. The Coordinator web UI is displayed.

-  Method 2 (for versions earlier than MRS 3.\ *x*)

   #. Log in to MRS Manager and choose **Services**.
   #. Select **Presto**. In the **Presto Summary** area, click **Coordinator (Active)** next to **Presto Web UI**. The Presto web UI is displayed.

      .. note::

         When accessing the Presto web UI for the first time, you must add the address to the trusted site list.

-  Method 3 (for MRS 1.9.2 or later)

   #. Log in to the MRS console, click the target cluster name to go to the cluster details page, and click the **Components** tab.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   #. Click **Presto**. In the **Presto Summary** area, click **Coordinator (Active)** next to **Presto Web UI**. The Presto web UI is displayed.
