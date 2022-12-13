:original_name: mrs_01_0394.html

.. _mrs_01_0394:

Stopping or Uninstalling the Flume Client
=========================================

Scenario
--------

You can stop and start the Flume client or uninstall the Flume client when the Flume data ingestion channel is not required.

Procedure
---------

-  Stop the Flume client of the Flume role.

   Assume that the Flume client installation path is **/opt/FlumeClient**. Run the following command to stop the Flume client:

   **cd /opt/FlumeClient/fusioninsight-flume-**\ *Flume component version number*\ **/bin**

   **./flume-manage.sh stop**

   If the following information is displayed after the command execution, the Flume client is successfully stopped.

   .. code-block::

      Stop Flume PID=120689 successful..

   .. note::

      The Flume client will be automatically restarted after being stopped. If you do not need automatic restart, run the following command:

      **./flume-manage.sh stop force**

      If you want to restart the Flume client, run the following command:

      **./flume-manage.sh start force**

-  Uninstall the Flume client of the Flume role.

   Assume that the Flume client installation path is **/opt/FlumeClient**. Run the following command to uninstall the Flume client:

   **cd /opt/FlumeClient/fusioninsight-flume-**\ *Flume component version number*\ **/inst**

   **./uninstall.sh**
