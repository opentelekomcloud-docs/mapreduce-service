:original_name: admin_guide_000003.html

.. _admin_guide_000003:

Querying the FusionInsight Manager Version
==========================================

By viewing the FusionInsight Manager version, you can prepare for system upgrade and routine maintenance.

-  Using the GUI:

   Log in to FusionInsight Manager. On the home page, click |image1| in the upper right corner and choose **About** from the drop-down list. In the dialog box that is displayed, view the FusionInsight Manager version.

-  Using the CLI

   #. Log in to the FusionInsight Manager active management node as user **root**.

   #. Run the following commands to check the version and platform information of FusionInsight Manager:

      **su - omm**

      **cd ${BIGDATA_HOME}/om-server/om/sbin/pack**

      **./queryManager.sh**

      The following information is displayed:

      .. code-block::

              Version             Package                                                          Cputype
              ***                 FusionInsight_Manager_***                                        x86_64

      .. note::

         **\**\*** indicates the version number. Replace it with the actual version number.

.. |image1| image:: /_static/images/en-us_image_0000001438954277.png
