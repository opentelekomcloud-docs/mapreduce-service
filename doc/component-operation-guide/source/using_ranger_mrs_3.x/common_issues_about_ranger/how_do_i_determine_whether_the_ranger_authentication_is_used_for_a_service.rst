:original_name: mrs_01_1868.html

.. _mrs_01_1868:

How Do I Determine Whether the Ranger Authentication Is Used for a Service?
===========================================================================

Question
--------

How do I determine whether the Ranger authentication is enabled for a service that supports the authentication?

Answer
------

Log in to FusionInsight Manager and choose **Cluster** > **Services** > *Name of the desired service*. On the service details page, click **More** and check whether the **Enable Ranger** option is available.

-  If yes, the Ranger authentication plug-in is not enabled for the service. You can click **Enable Ranger** to enable the function.
-  If no, the Ranger authentication plug-in has been enabled for the service. You can configure the permission policy for accessing the service resources on the Ranger management page.
