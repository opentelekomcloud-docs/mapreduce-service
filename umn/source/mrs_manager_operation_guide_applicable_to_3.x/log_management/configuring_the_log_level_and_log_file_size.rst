:original_name: admin_guide_000195.html

.. _admin_guide_000195:

Configuring the Log Level and Log File Size
===========================================

Scenario
--------

You can change the log levels of MRS Manager. For a specific service, you can change the log level and the log file size to prevent the failure in saving logs due to insufficient disk space.

Impact on the System
--------------------

The services need to be restarted for the new configuration to take effect. During the restart, the services are unavailable.

Changing the MRS Manager Log Level
----------------------------------

#. Log in to the active management node as user **omm**.

#. Run the following command to switch to the required directory:

   **cd ${BIGDATA_HOME}/om-server/om/sbin**

#. Run the following command to change the log level:

   **./setLogLevel.sh**\ *Log level parameters*

   The priorities of log levels are FATAL, ERROR, WARN, INFO, and DEBUG in descending order. Logs whose levels are higher than or equal to the set level are printed. The number of printed logs decreases as the configured log level increases.

   -  **DEFAULT**: After this parameter is set, the default log level is used.
   -  **FATAL**: critical error log level. After this parameter is set, only logs of the **FATAL** level are printed.
   -  **ERROR**: error log level. After this parameter is set, logs of the **ERROR** and **FATAL** levels are printed.
   -  **WARN**: warning log level. After this parameter is set, logs of the **WARN**, **ERROR**, and **FATAL** levels are printed.
   -  **INFO** (default): informational log level. After this parameter is set, logs of the **INFO**, **WARN**, **ERROR**, and **FATAL** levels are printed.
   -  **DEBUG**: debugging log level. After this parameter is set, logs of the **DEBUG**, **INFO**, **WARN**, **ERROR**, and **FATAL** levels are printed.
   -  **TRACE**: tracing log level. After this parameter is set, logs of the **TRACE**, **DEBUG**, **INFO**, **WARN**, **ERROR**, and **FATAL** levels are printed.

   .. note::

      The log levels of components are different from those defined in open-source code.

#. Download and view logs to verify that the log level settings have taken effect. For details, see :ref:`Log <admin_guide_000073>`.

Changing the Service Log Level and Log File Size
------------------------------------------------

.. note::

   KrbServer, LdapServer, and DBService do not support the changing of service log levels and log file sizes.

#. Log in to MRS Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Services**.
#. Click a service in the service list. On the displayed page, click the **Configuration** page.
#. On the displayed page, click the **All Configuration** tab. Expand the role instance displayed on the left of the page. Click **Log** of the role to be modified.
#. Search for each parameter and obtain the parameter description. On the parameter configuration page, select the required log level or change the log file size. The unit of the log file size is MB.

   .. important::

      -  The system automatically deletes logs based on the configured log size. To save more information, set the log file size to a larger value. To ensure the integrity of log files, you are advised to manually back up the log files to another directory based on the actual service volume before the log files are cleared according to clearance rules.
      -  Some services do not support change of the log level on the UI.

#. Click **Save**. In the **Save Configuration** dialog box, click **OK**.
#. Download and view logs to verify that the log level settings have taken effect.
