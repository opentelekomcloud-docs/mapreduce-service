:original_name: mrs_01_0133.html

.. _mrs_01_0133:

Hue Common Parameters
=====================

Page Access
-----------

Go to the **All Configurations** page of the Hue service by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

Parameter Description
---------------------

For details about Hue common parameters, see :ref:`Table 1 <mrs_01_0133__t7018ca0013604e85adf24a3af0e1e47d>`.

.. _mrs_01_0133__t7018ca0013604e85adf24a3af0e1e47d:

.. table:: **Table 1** Hue common parameters

   +--------------------------------+----------------------------------+-----------------+-----------------+
   | Configuration                  | Description                      | Default Value   | Value Range     |
   +================================+==================================+=================+=================+
   | HANDLER_ACCESSLOG_LEVEL        | Hue access log level.            | DEBUG           | -  ERROR        |
   |                                |                                  |                 | -  WARN         |
   |                                |                                  |                 | -  INFO         |
   |                                |                                  |                 | -  DEBUG        |
   +--------------------------------+----------------------------------+-----------------+-----------------+
   | HANDLER_AUDITSLOG_LEVEL        | Hue audit log level.             | DEBUG           | -  ERROR        |
   |                                |                                  |                 | -  WARN         |
   |                                |                                  |                 | -  INFO         |
   |                                |                                  |                 | -  DEBUG        |
   +--------------------------------+----------------------------------+-----------------+-----------------+
   | HANDLER_ERRORLOG_LEVEL         | Hue error log level.             | ERROR           | -  ERROR        |
   |                                |                                  |                 | -  WARN         |
   |                                |                                  |                 | -  INFO         |
   |                                |                                  |                 | -  DEBUG        |
   +--------------------------------+----------------------------------+-----------------+-----------------+
   | HANDLER_LOGFILE_LEVEL          | Hue run log level.               | INFO            | -  ERROR        |
   |                                |                                  |                 | -  WARN         |
   |                                |                                  |                 | -  INFO         |
   |                                |                                  |                 | -  DEBUG        |
   +--------------------------------+----------------------------------+-----------------+-----------------+
   | HANDLER_LOGFILE_MAXBACKUPINDEX | Maximum number of Hue log files. | 20              | 1 to 999        |
   +--------------------------------+----------------------------------+-----------------+-----------------+
   | HANDLER_LOGFILE_SIZE           | Maximum size of a Hue log file.  | 5 MB            | ``-``           |
   +--------------------------------+----------------------------------+-----------------+-----------------+
