:original_name: mrs_01_0134.html

.. _mrs_01_0134:

Using HiveQL Editor on the Hue Web UI
=====================================

Scenario
--------

Users can use the Hue web UI to execute HiveQL statements in an MRS cluster.

Access Editor
-------------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

#. In the navigation tree on the left, click |image1| and choose **Hive**. The **Hive** page is displayed.

   **Hive** supports the following functions:

   -  Executes and manages HiveQL statements.
   -  Views the HiveQL statements saved by the current user in **Saved Queries**.
   -  Queries HiveQL statements executed by the current user in **Query History**.

Executing HiveQL Statements
---------------------------

#. Select a Hive database from the **Database** drop-down list box. The default database is **default**.

   The system displays all available tables. You can enter a keyword of the table name to search for the desired table.

#. Click the desired table name. All columns in the table are displayed.

   Move the cursor to the row where the table or column is located and click |image2|. Column details are displayed.

#. Enter the query statements in the area for editing HiveQL statements.

#. Click |image3| to execute the HiveQL statements.

   .. note::

      -  If you want to use the entered HiveQL statements again, click |image4| to save them.

      -  Advanced query configuration:

         Click |image5| in the upper right corner to configure information such as files, functions, and settings.

      -  Viewing the information of shortcut keys:

         Click |image6| in the upper right corner to view the syntax and keyboard shortcut information.

      -  To delete an entered HiveQL statement, click the triangle next to |image7| and select **Clear**.

      -  Viewing history:

         Click **Query History** to view the HiveQL running status. You can view the history of all the statements or only the saved statements. If many historical records exist, you can enter keywords in the text box to search for desired records.

Viewing Execution Results
-------------------------

#. View the execution results below the execution area on **Hive**. The **Query History** tab page is displayed by default.
#. Click a result to view the execution result of the executed statement.

Managing Query Statements
-------------------------

#. Click **Saved Queries**.
#. Click a saved statement. The system automatically adds the statement to the editing area.

Modifying the Session Configuration of the Hue Editor
-----------------------------------------------------

#. On the editor page, click |image8|.

#. Click |image9| on the right of **Files**, and then click |image10| to select files.

   You can click |image11| next to **Files** to add a file resource.

#. In the **Functions** |image12| area, enter a user-defined name and the class name of the function.

   You can click |image13| next to **Functions** to add a customized function.

#. In the **Settings** |image14| area, enter the Hive parameter name in the **Key**, and value in **Value**. The current Hive session connects to Hive based on the customized configuration.

   You can click |image15| to add a parameter.

.. |image1| image:: /_static/images/en-us_image_0000001296219476.png
.. |image2| image:: /_static/images/en-us_image_0000001349259145.png
.. |image3| image:: /_static/images/en-us_image_0000001349139561.jpg
.. |image4| image:: /_static/images/en-us_image_0000001348739873.png
.. |image5| image:: /_static/images/en-us_image_0000001296059844.png
.. |image6| image:: /_static/images/en-us_image_0000001349059685.png
.. |image7| image:: /_static/images/en-us_image_0000001349059689.jpg
.. |image8| image:: /_static/images/en-us_image_0000001295740036.jpg
.. |image9| image:: /_static/images/en-us_image_0000001296219480.jpg
.. |image10| image:: /_static/images/en-us_image_0000001296059848.jpg
.. |image11| image:: /_static/images/en-us_image_0000001296219480.jpg
.. |image12| image:: /_static/images/en-us_image_0000001296219480.jpg
.. |image13| image:: /_static/images/en-us_image_0000001296219480.jpg
.. |image14| image:: /_static/images/en-us_image_0000001296219480.jpg
.. |image15| image:: /_static/images/en-us_image_0000001296219480.jpg
