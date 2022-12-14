:original_name: mrs_01_24020.html

.. _mrs_01_24020:

Creating an Application on the Flink Web UI
===========================================

Scenario
--------

Applications can be used to isolate different upper-layer services.

Creating an Application
-----------------------

#. Access the Flink web UI as a user with **FlinkServer Admin Privilege**. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.

#. Choose **System Management** > **Application Management**.

#. Click **Create Application**. On the displayed page, set parameters by referring to :ref:`Table 1 <mrs_01_24020__table2048293612324>` and click **OK**.

   .. _mrs_01_24020__table2048293612324:

   .. table:: **Table 1** Parameters for creating an application

      +-------------+------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter   | Description                                                                                                                                    |
      +=============+================================================================================================================================================+
      | Application | Name of the application to be created. The name can contain a maximum of 32 characters. Only letters, digits, and underscores (_) are allowed. |
      +-------------+------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description | Description of the application to be created. The value can contain a maximum of 85 characters.                                                |
      +-------------+------------------------------------------------------------------------------------------------------------------------------------------------+

   After the application is created, you can switch to the application to be operated in the upper left corner of the Flink web UI and develop jobs.
