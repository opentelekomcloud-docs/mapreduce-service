:original_name: mrs_01_0245.html

.. _mrs_01_0245:

Managing Services
=================

You can perform the following operations on MRS Manager:

-  Start the service in the **Stopped**, **Stop Failed**, or **Start Failed** state to use the service.
-  Stop the services or stop abnormal services.
-  Restart abnormal services or configure expired services to restore or enable the services.

Procedure
---------

#. On MRS Manager page, click **Services**.

#. Locate the row that contains the target service, **Start**, **Stop**, or **Restart** to start, stop, or restart the service.

   Services are interrelated. If a service is started, stopped, and restarted, services dependent on it will be affected.

   The services will be affected in the following ways:

   -  If a service is to be started, the lower-layer services dependent on it must be started first.
   -  If a service is stopped, the upper-layer services dependent on it are unavailable.
   -  If a service is restarted, the running upper-layer services dependent on it must be restarted.
