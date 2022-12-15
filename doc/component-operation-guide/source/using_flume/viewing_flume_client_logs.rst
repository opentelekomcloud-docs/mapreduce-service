:original_name: mrs_01_0393.html

.. _mrs_01_0393:

Viewing Flume Client Logs
=========================

Scenario
--------

You can view logs to locate faults.

Prerequisites
-------------

The Flume client has been installed.

Procedure
---------

#. Go to the Flume client log directory (**/var/log/Bigdata** by default).

#. Run the following command to view the log file:

   **ls -lR flume-client-\***

   A log file is shown as follows:

   .. code-block::

      flume-client-1/flume:
      total 7672
      -rw-------. 1 root root       0 Sep  8 19:43 Flume-audit.log
      -rw-------. 1 root root 1562037 Sep 11 06:05 FlumeClient.2017-09-11_04-05-09.[1].log.zip
      -rw-------. 1 root root 6127274 Sep 11 14:47 FlumeClient.log
      -rw-------. 1 root root    2935 Sep  8 22:20 flume-root-20170908202009-pid72456-gc.log.0.current
      -rw-------. 1 root root    2935 Sep  8 22:27 flume-root-20170908202634-pid78789-gc.log.0.current
      -rw-------. 1 root root    4382 Sep  8 22:47 flume-root-20170908203137-pid84925-gc.log.0.current
      -rw-------. 1 root root    4390 Sep  8 23:46 flume-root-20170908204918-pid103920-gc.log.0.current
      -rw-------. 1 root root    3196 Sep  9 10:12 flume-root-20170908215351-pid44372-gc.log.0.current
      -rw-------. 1 root root    2935 Sep  9 10:13 flume-root-20170909101233-pid55119-gc.log.0.current
      -rw-------. 1 root root    6441 Sep  9 11:10 flume-root-20170909101631-pid59301-gc.log.0.current
      -rw-------. 1 root root       0 Sep  9 11:10 flume-root-20170909111009-pid119477-gc.log.0.current
      -rw-------. 1 root root   92896 Sep 11 13:24 flume-root-20170909111126-pid120689-gc.log.0.current
      -rw-------. 1 root root    5588 Sep 11 14:46 flume-root-20170911132445-pid42259-gc.log.0.current
      -rw-------. 1 root root    2576 Sep 11 13:24 prestartDetail.log
      -rw-------. 1 root root    3303 Sep 11 13:24 startDetail.log
      -rw-------. 1 root root    1253 Sep 11 13:24 stopDetail.log

      flume-client-1/monitor:
      total 8
      -rw-------. 1 root root  141 Sep  8 19:43 flumeMonitorChecker.log
      -rw-------. 1 root root 2946 Sep 11 13:24 flumeMonitor.log

   In the log file, **FlumeClient.log** is the run log of the Flume client.
