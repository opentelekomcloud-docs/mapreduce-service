:original_name: mrs_01_0137.html

.. _mrs_01_0137:

Using Job Browser on the Hue Web UI
===================================

Scenario
--------

Users can use the Hue web UI to query all jobs in an MRS cluster.

Accessing Job Browser
---------------------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

#. Click |image1|.

   View the jobs in the current cluster.

   .. note::

      The number on **Job Browser** indicates the total number of jobs in the cluster.

   **Job Browser** displays the following job information:

   .. table:: **Table 1** MRS job attributes

      +-----------+-------------------------------------------------------------------+
      | Attribute | Description                                                       |
      +===========+===================================================================+
      | Name      | Job name                                                          |
      +-----------+-------------------------------------------------------------------+
      | User      | User who starts a job                                             |
      +-----------+-------------------------------------------------------------------+
      | Type      | Job type                                                          |
      +-----------+-------------------------------------------------------------------+
      | Status    | Job status, including **Succeeded**, **Running**, and **Failed**. |
      +-----------+-------------------------------------------------------------------+
      | Progress  | Job running progress                                              |
      +-----------+-------------------------------------------------------------------+
      | Group     | Group to which a job belongs                                      |
      +-----------+-------------------------------------------------------------------+
      | Start     | Start time of a job                                               |
      +-----------+-------------------------------------------------------------------+
      | Duration  | Job running duration                                              |
      +-----------+-------------------------------------------------------------------+
      | Id        | Job ID, which is generated by the system automatically.           |
      +-----------+-------------------------------------------------------------------+

   .. note::

      If the MRS cluster has Spark, the **Spark-JDBCServer** job is started by default to execute tasks.

Searching for Jobs
------------------

#. In the search box of **Job Browser**, enter the specified character. The system automatically searches for all jobs that contain the keyword by ID, name, or user.
#. Clear the search criteria. The system displays all jobs.

Querying Job Details
--------------------

#. In the job list on the **Job Browser** page, click the row that contains the desired job to view details.
#. On the **Metadata** tab page, you can view the metadata of the job.

   .. note::

      You can click **Log** to open the job running log.

.. |image1| image:: /_static/images/en-us_image_0000001295930704.png
