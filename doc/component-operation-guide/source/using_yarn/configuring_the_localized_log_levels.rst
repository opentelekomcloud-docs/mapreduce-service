:original_name: mrs_01_0867.html

.. _mrs_01_0867:

Configuring the Localized Log Levels
====================================

This section applies to clusters of MRS 3.\ *x* or later.

Scenarios
---------

The default log level of localized container is **INFO**. You can change the log level by configuring **yarn.nodemanager.container-localizer.java.opts**.

Configuration Description
-------------------------

On Manager, choose **Cluster** > *Name of the desired cluster* > **Service** > **Yarn** > **Configuration**. Select **All Configurations** and set the following parameters in the configuration file **yarn-site.xml** of NodeManager to change the log level.

.. table:: **Table 1** Parameter description

   +------------------------------------------------+-------------------------------------------------------------------------------------+---------------------------------------------------+
   | Parameter                                      | Description                                                                         | Default Value                                     |
   +================================================+=====================================================================================+===================================================+
   | yarn.nodemanager.container-localizer.java.opts | The additional **jvm** parameters are provided for the localized container process. | -Xmx256m -Djava.security.krb5.conf=${KRB5_CONFIG} |
   +------------------------------------------------+-------------------------------------------------------------------------------------+---------------------------------------------------+

The default value is **-Xmx256m -Djava.security.krb5.conf=${KRB5_CONFIG}** and the default log level is info. To change the localized log level of the container, add the following content:

.. code-block::

   -Dhadoop.root.logger=<LOG_LEVEL>,localizationCLA

**Example:**

To change the local log level to **DEBUG**, set the parameter as follows:

.. code-block::

   -Xmx256m -Dhadoop.root.logger=DEBUG,localizationCLA

.. note::

   Allowed log levels are as follows: FATAL, ERROR, WARN, INFO, DEBUG, TRACE, and ALL.
