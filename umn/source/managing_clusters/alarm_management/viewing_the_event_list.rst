:original_name: mrs_01_0602.html

.. _mrs_01_0602:

Viewing the Event List
======================

The event list displays information about all events in a cluster, such as service restart and service termination.

Events are listed in chronological order by default in the event list, with the most recent events displayed at the top.

:ref:`Table 1 <mrs_01_0602__en-us_topic_0173397435_table5924273517010>` describes various fields for an event.

.. _mrs_01_0602__en-us_topic_0173397435_table5924273517010:

.. table:: **Table 1** Event description

   +-----------------------------------+--------------------------------------------------------------------------+
   | Parameter                         | Description                                                              |
   +===================================+==========================================================================+
   | Event ID                          | Specifies the ID of an event.                                            |
   +-----------------------------------+--------------------------------------------------------------------------+
   | Event Severity                    | Specifies the event severity.                                            |
   |                                   |                                                                          |
   |                                   | In versions earlier than MRS 3.x, the cluster event level is as follows: |
   |                                   |                                                                          |
   |                                   | -  Critical                                                              |
   |                                   | -  Major                                                                 |
   |                                   | -  Minor                                                                 |
   |                                   | -  Suggestion                                                            |
   |                                   |                                                                          |
   |                                   | In MRS 3.x or later, the event level of a cluster is as follows:         |
   |                                   |                                                                          |
   |                                   | -  Critical                                                              |
   |                                   | -  Major                                                                 |
   |                                   | -  Minor                                                                 |
   |                                   | -  Suggestion                                                            |
   +-----------------------------------+--------------------------------------------------------------------------+
   | Event Name                        | Name of the generated event.                                             |
   +-----------------------------------+--------------------------------------------------------------------------+
   | Generated                         | Time when the event is generated.                                        |
   +-----------------------------------+--------------------------------------------------------------------------+
   | Location                          | Specifies the detailed information for locating the event,               |
   +-----------------------------------+--------------------------------------------------------------------------+

.. table:: **Table 2** Icon description

   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Icon                              | Description                                                                                                                                                                                           |
   +===================================+=======================================================================================================================================================================================================+
   | |image1|                          | Select an interval for refreshing the event list from the drop-down list.                                                                                                                             |
   |                                   |                                                                                                                                                                                                       |
   |                                   | -  Refresh every 30s                                                                                                                                                                                  |
   |                                   | -  Refresh every 60s                                                                                                                                                                                  |
   |                                   | -  Stop refreshing                                                                                                                                                                                    |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |image2|                          | Click |image3| to manually refresh the event list.                                                                                                                                                    |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Advanced Search                   | Click **Advanced Search**. In the displayed event search area, set search criteria and click **Search** to view the information about specified events. Click **Reset** to clear the search criteria. |
   +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Exporting events
----------------

#. Choose **Clusters > Active Clusters** and click a cluster name to go to the cluster details page.
#. Click **Alarm Management** > **Events**.
#. Click **Export All**.
#. In the displayed dialog box, select the type and click **OK**.

Common Events
-------------

.. table:: **Table 3** Common events

   ======== ==========================================================
   Event ID Event Name
   ======== ==========================================================
   12019    Stop Service
   12020    Delete Service
   12021    Stop RoleInstance
   12022    Delete RoleInstance
   12023    Delete Node
   12024    Restart Service
   12025    Restart RoleInstance
   12026    Manager Switchover
   12065    Process Restart
   12070    Job Running Succeeded
   12071    Job Running Failed
   12072    Job killed
   12086    Agent Restart
   14005    NameNode Switchover
   14028    HDFS DiskBalancer Task
   14029    Active NameNode enters safe mode and generates new Fsimage
   17001    Oozie Workflow Execution Failure
   17002    Oozie Scheduled Job Execution Failure
   18001    ResourceManager Switchover
   18004    JobHistoryServer Switchover
   19001    HMaster Failover
   20003    Hue Failover
   24002    Flume Channel Overflow
   25001    LdapServer Failover
   27000    DBServer Switchover
   38003    Adjusts the topic data storage period
   43014    Spark Data Skew
   43015    Spark SQL Large Query Results
   43016    Spark SQL Execution Timeout
   43024    Start JDBCServer
   43025    Stop JDBCServer
   43026    ZooKeeper Connection Succeeded
   43027    Zookeeper Connection Failed
   ======== ==========================================================

.. |image1| image:: /_static/images/en-us_image_0000001295898004.png
.. |image2| image:: /_static/images/en-us_image_0000001296217480.png
.. |image3| image:: /_static/images/en-us_image_0000001348737865.png
