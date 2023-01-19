:original_name: mrs_01_2393.html

.. _mrs_01_2393:

Enabling Ranger Authentication
==============================

Scenario
--------

This section guides you how to enable Ranger authentication. Ranger authentication is enabled by default in security mode and disabled by default in normal mode.

Procedure
---------

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > *Name of the service for which Ranger authentication is enabled*.

#. In the upper right corner of the **Dashboard** page, click **More** and select **Enable Ranger**. In the displayed dialog box, enter the password and click **OK**. After the operation is successful, click **Finish**.

   .. note::

      If **Enable Ranger** is dimmed, Ranger authentication is enabled, as shown in :ref:`Figure 1 <mrs_01_2393__en-us_topic_0000001173949712_fig14437127109>`.

   .. _mrs_01_2393__en-us_topic_0000001173949712_fig14437127109:

   .. figure:: /_static/images/en-us_image_0000001349259205.png
      :alt: **Figure 1** Enabling Ranger Authentication

      **Figure 1** Enabling Ranger Authentication

#. Perform a rolling service restart or restart the service.
