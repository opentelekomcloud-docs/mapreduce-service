:original_name: mrs_01_24813.html

.. _mrs_01_24813:

Purging Historical Loader Data
==============================

This section applies to MRS 3.2.0 or later.

Scenario
--------

Loader accumulates a large amount of historical data during service running. The historical data may affect job submission, running, and status query, and even cause page freezing and job running failures. Therefore, you need to properly configure the historical data pruge policy based on the Loader service data volume.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Cluster** > **Services** > **Loader** and click the **Configurations** tab and then **All Configurations**. In the navigation pane on the left, choose **LoaderServer(Role)** > **Purge**. Then adjust the parameter settings shown in the following figure by referring to :ref:`Table 1 <mrs_01_24813__table48037266219>`.

   |image1|

   .. _mrs_01_24813__table48037266219:

   .. table:: **Table 1** Parameters for purging historical Loader data

      +------------------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------+
      | Parameter                          | Description                                                                                                               | Recommended Value |
      +====================================+===========================================================================================================================+===================+
      | loader.submission.purge.interval   | Interval for invoking the purge task, in minutes.                                                                         | 60                |
      +------------------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------+
      | loader.submission.purge.limited    | Number of submissions that are retained during the purge. This prevents historical job records from being totally purged. | 0                 |
      +------------------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------+
      | loader.submission.purge.record.max | Maximum number of records that can be retained in a Loader job. Value **0** indicates that the number is not limited.     | 7                 |
      +------------------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------+
      | loader.submission.purge.threshold  | Duration for retaining historical records, in hours.                                                                      | 24                |
      +------------------------------------+---------------------------------------------------------------------------------------------------------------------------+-------------------+

#. Click **Save**.

#. Click **Dashboard** to go to the Loader service page. Click **More** and select **Restart Service**. Verify the identity and click **OK**. Wait until the restart is successful.

.. |image1| image:: /_static/images/en-us_image_0000001532549720.png
