:original_name: admin_guide_000064.html

.. _admin_guide_000064:

Distribution
============

Log in to FusionInsight Manager and choose **Hosts** > **Resource Overview**. On the **Resource Overview** page that is displayed, click the **Distribution** tab to view resource distribution of each cluster. By default, the monitoring data of the past one hour (**1h**) is displayed. You can click |image1| to customize a time range. Time range options are **1h**, **2h**, **6h**, **12h**, **1d**, **1w**, and **1m**.

.. _admin_guide_000064__fig10343181024812:

.. figure:: /_static/images/en-us_image_0000001087459671.png
   :alt: **Figure 1** Distribution tab

   **Figure 1** Distribution tab

-  You can click **Select Metric** to customize the metric to monitor. :ref:`Table 1 <admin_guide_000064__table1190415121488>` describes all the metrics that you can select. After you select a metric, the host distribution in each range of the metric is displayed.
-  When you hover your cursor over a color column, the number of hosts in the current metric range is displayed. See :ref:`Figure 1 <admin_guide_000064__fig10343181024812>`. You can click a color column to view the list of hosts in the metric range.

   -  You can click a host name in the **Host Name** column to access the host details page.
   -  You can click **View Trends** in the **Operation** column of a host to view the maximum, minimum, and average values of the current metric in the cluster as well as the value of the current host. In the current cluster, if you have selected **Host CPU-Memory-Disk Usage**, **View Trends** is unavailable.

-  You can click **Export Data** to export the maximum, minimum, and average values of the current metric of all nodes in the cluster within the time range you have specified.

.. _admin_guide_000064__table1190415121488:

.. table:: **Table 1** Metrics

   +-----------------------------------+--------------------------------------------------------------+
   | Category                          | Metric                                                       |
   +===================================+==============================================================+
   | Process                           | -  Number of Running Processes                               |
   |                                   | -  Total Number of Processes                                 |
   |                                   | -  Total Number of omm Processes                             |
   |                                   | -  Uninterruptible Sleep Process                             |
   +-----------------------------------+--------------------------------------------------------------+
   | Network Status                    | -  Host Network Packet Collisions                            |
   |                                   | -  Number of LAST_ACK States                                 |
   |                                   | -  Number of CLOSING States                                  |
   |                                   | -  Number of LISTENING States                                |
   |                                   | -  Number of CLOSED States                                   |
   |                                   | -  Number of ESTABLISHED States                              |
   |                                   | -  Number of SYN_RECV States                                 |
   |                                   | -  Number of TIME_WAITING States                             |
   |                                   | -  Number of FIN_WAIT2 States                                |
   |                                   | -  Number of FIN_WAIT1 States                                |
   |                                   | -  Number of CLOSE_WAIT States                               |
   |                                   | -  DNS Name Resolution Duration                              |
   |                                   | -  TCP Ephemeral Port Usage                                  |
   |                                   | -  Host Network Packet Frame Errors                          |
   +-----------------------------------+--------------------------------------------------------------+
   | Network Reading                   | -  Host Network Read Packets                                 |
   |                                   | -  Host Network Read Dropped Packets                         |
   |                                   | -  Host Network Read Error Packets                           |
   |                                   | -  Host Network Rx Speed                                     |
   +-----------------------------------+--------------------------------------------------------------+
   | Disk                              | -  Host Disk Write Speed                                     |
   |                                   | -  Host Used Disk                                            |
   |                                   | -  Host Free Disk                                            |
   |                                   | -  Host Disk Read Speed                                      |
   |                                   | -  Host Disk Usage                                           |
   +-----------------------------------+--------------------------------------------------------------+
   | Memory                            | -  Free Memory                                               |
   |                                   | -  Cache Memory Size                                         |
   |                                   | -  Total Kernel Cache Memory Size                            |
   |                                   | -  Shared Memory Size                                        |
   |                                   | -  Host Memory Usage                                         |
   |                                   | -  Used Memory                                               |
   +-----------------------------------+--------------------------------------------------------------+
   | Network Writing                   | -  Host Network Write Packets                                |
   |                                   | -  Host Network Write Error Packets                          |
   |                                   | -  Host Network Tx Speed                                     |
   |                                   | -  Host Network Write Dropped Packets                        |
   +-----------------------------------+--------------------------------------------------------------+
   | CPU                               | -  CPU Usage of Processes Whose Priorities Have Been Changed |
   |                                   | -  CPU Usage of User Space Processes                         |
   |                                   | -  CPU Usage of Kernel Space Processes                       |
   |                                   | -  Host CPU Usage                                            |
   |                                   | -  CPU Total Time                                            |
   |                                   | -  CPU Idle Time                                             |
   +-----------------------------------+--------------------------------------------------------------+
   | Host Status                       | -  Host File Handle Usage                                    |
   |                                   | -  Average OS Load in 1 Minute                               |
   |                                   | -  Average OS Load in 5 Minutes                              |
   |                                   | -  Average OS Load in 15 Minutes                             |
   |                                   | -  Host PID Usage                                            |
   +-----------------------------------+--------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001318123498.png
