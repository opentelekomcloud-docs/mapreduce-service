:original_name: mrs_01_0371.html

.. _mrs_01_0371:

Using HiveQL Editor on the Hue Web UI
=====================================

Scenario
--------

Users can use the Hue web UI to execute HiveQL statements in a cluster.

For versions earlier than MRS 1.9.2, MRS clusters with Kerberos authentication enabled support this function.

Accessing Query Editors
-----------------------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0370>`.

#. Choose **Query Editors** > **Hive**. The **Hive** page is displayed.

   **Hive** supports the following functions:

   -  Executes and manages HiveQL statements.
   -  View the HiveQL statements saved by the current user in **Saved Queries**.
   -  Query HiveQL statements executed by the current user in **Query History**.
   -  Click |image1| to display all databases included in **Databases** of Hive.

Executing HiveQL Statements
---------------------------

#. Choose **Query Editors > Hive**. The **Hive** page is displayed.

#. Click |image2| and select a database from **Databases**. The default database is **default**.

   The system displays all available tables in the database. You can enter a keyword of the table name to search for the desired table.

#. Click the desired table name. All columns in the table are displayed.

   Move the cursor to the row of the table and click |image3|. Column details are displayed.

#. Enter the query statements in the area for editing HiveQL statements.

   Click |image4| and select **Explain**. The editor checks the syntax and execution plan of the entered statements. If the statements have syntax errors, the editor reports **Error while compiling statement**.

#. Click |image5| and select the engine for executing the HiveQL statements.

   -  **mr**: MapReduce computing framework
   -  **spark**: Spark computing framework
   -  **tez**: Tez computing framework

      .. note::

         Tez is applicable to MRS 1.9.\ *x* and later versions.

#. Click |image6| to execute the HiveQL statements.

   .. note::

      -  If you want to use the entered HiveQL statements again, click |image7| to save them.

      -  To format HiveQL statements, click |image8| and select **Format**.

      -  To delete an entered HiveQL statement, click |image9| and select **Clear**.

      -  Clear the entered statement and execute a new statement. Click |image10| and select **New query**.

      -  Viewing history:

         Click **Query History** to view the HiveQL running status. You can view the history of all the statements or only the saved statements. If many historical records exist, you can enter keywords in the text box to search for desired records.

      -  Advanced query configuration:

         Click |image11| in the upper right corner to configure information such as files, functions, and settings.

      -  Viewing the information of shortcut keys:

         Click |image12| in the upper right corner to view all shortcut keys.

Viewing Execution Results
-------------------------

#. In the **Hive** execution area, **Query History** is displayed by default.
#. Click **Results** to view the execution result of the executed statement.

Managing Query Statements
-------------------------

#. Choose **Query Editors > Hive**. The **Hive** page is displayed.

#. Click **Saved Queries**.

   Click a saved statement. The system automatically adds the statement to the editing area.

Modifying Query Editors Settings
--------------------------------

#. On the **Hive** tab page, click |image13|.

#. Click |image14| on the right of **Files** and click |image15| to specify the directory for storing the file.

   You can click |image16| to add a file resource.

#. Click |image17| on the right of **Functions** and enter the names of user-defined function and function class.

   You can click |image18| to add a customized function.

#. Click |image19| on the right of **Settings**, enter the Hive parameter name in the **Key**, and value in **Value**. The current Hive session connects to Hive based on the customized configuration.

   You can click |image20| to add a parameter.

.. |image1| image:: /_static/images/en-us_image_0000001349289717.jpg
.. |image2| image:: /_static/images/en-us_image_0000001296090388.jpg
.. |image3| image:: /_static/images/en-us_image_0000001295930560.jpg
.. |image4| image:: /_static/images/en-us_image_0000001295930564.jpg
.. |image5| image:: /_static/images/en-us_image_0000001348770417.png
.. |image6| image:: /_static/images/en-us_image_0000001349289713.jpg
.. |image7| image:: /_static/images/en-us_image_0000001349170129.jpg
.. |image8| image:: /_static/images/en-us_image_0000001295930564.jpg
.. |image9| image:: /_static/images/en-us_image_0000001295930564.jpg
.. |image10| image:: /_static/images/en-us_image_0000001295930564.jpg
.. |image11| image:: /_static/images/en-us_image_0000001349289709.png
.. |image12| image:: /_static/images/en-us_image_0000001349090229.png
.. |image13| image:: /_static/images/en-us_image_0000001349170133.jpg
.. |image14| image:: /_static/images/en-us_image_0000001348770421.jpg
.. |image15| image:: /_static/images/en-us_image_0000001349170125.jpg
.. |image16| image:: /_static/images/en-us_image_0000001348770421.jpg
.. |image17| image:: /_static/images/en-us_image_0000001348770421.jpg
.. |image18| image:: /_static/images/en-us_image_0000001348770421.jpg
.. |image19| image:: /_static/images/en-us_image_0000001348770421.jpg
.. |image20| image:: /_static/images/en-us_image_0000001348770421.jpg
