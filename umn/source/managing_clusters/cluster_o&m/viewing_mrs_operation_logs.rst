:original_name: en-us_topic_0012808265.html

.. _en-us_topic_0012808265:

Viewing MRS Operation Logs
==========================

You can view operation logs of clusters and jobs on the **Operation Logs** page. Log information is typically used for quickly locating faults in case of cluster exceptions, helping users resolve problems.

Operation Type
--------------

Currently, the following operation logs are provided by MRS. You can filter the logs in the search box.

-  Cluster operations

   -  Creating, deleting, scaling out, and scaling in a cluster
   -  Creating and deleting a directory, deleting a file

-  Job operations: Creating, stopping, and deleting a job
-  Data operations: IAM user tasks, adding user, and adding user group

Log Fields
----------

Logs are listed in chronological order by default in the log list, with the most recent logs displayed at the top.

:ref:`Table 1 <en-us_topic_0012808265__table5924273517010>` describes various fields in a log.

.. _en-us_topic_0012808265__table5924273517010:

.. table:: **Table 1** Log description

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                   |
   +===================================+===============================================================================================================================================================================================+
   | Operation Type                    | Various types of operations, including:                                                                                                                                                       |
   |                                   |                                                                                                                                                                                               |
   |                                   | -  Cluster operations                                                                                                                                                                         |
   |                                   | -  Job operations                                                                                                                                                                             |
   |                                   | -  Data operations                                                                                                                                                                            |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation IP                      | IP address where an operation is performed.                                                                                                                                                   |
   |                                   |                                                                                                                                                                                               |
   |                                   | .. note::                                                                                                                                                                                     |
   |                                   |                                                                                                                                                                                               |
   |                                   |    If an MRS cluster fails to be deployed, the cluster is automatically deleted, and the operation logs of the automatically deleted cluster do not contain the **Operation IP** of the user. |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Operation                         | Operation details. The value can contain a maximum of 2048 characters.                                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Time                              | Operation time. For a deleted cluster, only logs generated within the last six months are displayed. To view logs generated six months ago, contact technical support.                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** Icon description

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Icon                              | Description                                                                                                                                                                                       |
   +===================================+===================================================================================================================================================================================================+
   | |image1|                          | Select an operation type from the drop-down list box to filter logs.                                                                                                                              |
   |                                   |                                                                                                                                                                                                   |
   |                                   | -  **All Operation Types**: Filter all logs.                                                                                                                                                      |
   |                                   | -  **Cluster**: Filter logs for **Cluster**.                                                                                                                                                      |
   |                                   | -  **Job**: Filter logs for **Job**.                                                                                                                                                              |
   |                                   | -  **Data**: Filter logs for **Data**.                                                                                                                                                            |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |image2|                          | Filter logs by time.                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                   |
   |                                   | #. Click the input box.                                                                                                                                                                           |
   |                                   | #. Specify the date and time.                                                                                                                                                                     |
   |                                   | #. Click **OK**.                                                                                                                                                                                  |
   |                                   |                                                                                                                                                                                                   |
   |                                   | The left-side input box indicates the start time and the right-side one indicates the end time. The start time must be earlier than or equal to the end time. Otherwise, logs cannot be filtered. |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |image3|                          | Enter a keyword of the **Operation Details** in the search box and click |image4| to search for logs.                                                                                             |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |image5|                          | Click |image6| to manually refresh the log list.                                                                                                                                                  |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001349257469.png
.. |image2| image:: /_static/images/en-us_image_0000001348738189.jpg
.. |image3| image:: /_static/images/en-us_image_0000001349057965.png
.. |image4| image:: /_static/images/en-us_image_0000001349057965.png
.. |image5| image:: /_static/images/en-us_image_0000001349057929.png
.. |image6| image:: /_static/images/en-us_image_0000001349057929.png
