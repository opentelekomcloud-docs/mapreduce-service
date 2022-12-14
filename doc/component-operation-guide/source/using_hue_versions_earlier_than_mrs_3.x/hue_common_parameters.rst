:original_name: mrs_01_1021.html

.. _mrs_01_1021:

Hue Common Parameters
=====================

Navigation Path
---------------

For details about how to set parameters, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

Parameters
----------

.. table:: **Table 1** Hue common parameters

   +--------------------------------+----------------------------------+-----------------+-----------------+
   | Parameter                      | Description                      | Default Value   | Value Range     |
   +================================+==================================+=================+=================+
   | HANDLER_ACCESSLOG_LEVEL        | Hue access log level             | DEBUG           | -  ERROR        |
   |                                |                                  |                 | -  WARN         |
   |                                |                                  |                 | -  INFO         |
   |                                |                                  |                 | -  DEBUG        |
   +--------------------------------+----------------------------------+-----------------+-----------------+
   | HANDLER_AUDITSLOG_LEVEL        | Hue audit log level              | DEBUG           | -  ERROR        |
   |                                |                                  |                 | -  WARN         |
   |                                |                                  |                 | -  INFO         |
   |                                |                                  |                 | -  DEBUG        |
   +--------------------------------+----------------------------------+-----------------+-----------------+
   | HANDLER_ERRORLOG_LEVEL         | Hue error log level              | ERROR           | -  ERROR        |
   |                                |                                  |                 | -  WARN         |
   |                                |                                  |                 | -  INFO         |
   |                                |                                  |                 | -  DEBUG        |
   +--------------------------------+----------------------------------+-----------------+-----------------+
   | HANDLER_LOGFILE_LEVEL          | Hue run log level                | INFO            | -  ERROR        |
   |                                |                                  |                 | -  WARN         |
   |                                |                                  |                 | -  INFO         |
   |                                |                                  |                 | -  DEBUG        |
   +--------------------------------+----------------------------------+-----------------+-----------------+
   | HANDLER_LOGFILE_MAXBACKUPINDEX | Maximum number of Hue log files. | 20              | 1 to 999        |
   +--------------------------------+----------------------------------+-----------------+-----------------+
   | HANDLER_LOGFILE_SIZE           | Maximum size of a Hue log file.  | 5 MB            | ``-``           |
   +--------------------------------+----------------------------------+-----------------+-----------------+
