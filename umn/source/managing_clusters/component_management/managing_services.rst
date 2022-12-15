:original_name: mrs_01_0203.html

.. _mrs_01_0203:

Managing Services
=================

You can perform the following operations on MRS:

-  Start the service in the **Stopped**, **Stop Failed**, or **Failed to Start** state to use the service.
-  Stop the services or stop abnormal services.
-  Restart abnormal services or configure expired services to restore or enable the services.

Prerequisites
-------------

-  You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Impact on the System
--------------------

-  The stateful component cannot be added to the task node group.

Starting, Stopping, and Restarting a Service
--------------------------------------------

#. On the MRS cluster details page, click **Components**.

#. Locate the row that contains the target service, **Start**, **Stop**, and **Restart** to start, stop, or restart the service.

   Services are interrelated. If a service is started, stopped, and restarted, services dependent on it will be affected.

   The services will be affected in the following ways:

   -  If a service is to be started, the lower-layer services dependent on it must be started first.
   -  If a service is stopped, the upper-layer services dependent on it are unavailable.
   -  If a service is restarted, the running upper-layer services dependent on it must be restarted.
