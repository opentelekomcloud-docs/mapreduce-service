:original_name: mrs_01_2370.html

.. _mrs_01_2370:

Using the SparkSql Editor on the Hue Web UI
===========================================

Scenario
--------

You can use Hue to execute SparkSql statements in a cluster on a graphical user interface (GUI).

Configuring Spark2x
-------------------

Before using the SparkSql editor, you need to modify the Spark2x configuration.

#. Go to the Spark2x configuration page. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

#. Set the Spark2x multi-instance mode. Search for and modify the following parameters of the Spark2x service:

   ================================ =============================
   Parameter                        Value
   ================================ =============================
   spark.thriftserver.proxy.enabled false
   spark.scheduler.allocation.file  #{conf_dir}/fairscheduler.xml
   ================================ =============================

#. Go to the JDBCServer2x customization page and add the following customized items to the **spark.core-site.customized.configs** parameter:

   Set **hadoop.proxyuser.hue.groups** to **\***.

   Set **hadoop.proxyuser.hue.hosts** to **\***.

#. Save the configuration and restart the meta and Spark2x services.

Accessing the Editor
--------------------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

#. In the navigation tree on the left, click |image1| and choose **SparkSql**. The **SparkSql** page is displayed.

   **SparkSql** supports the following functions:

   -  Executes and manages SparkSql statements.
   -  Views the SparkSql statements saved by the current user in **Saved Queries**.
   -  Queries SparkSql statements executed by the current user in **Query History**.

Executing SparkSql Statements
-----------------------------

#. Select a SparkSql database from the **Database** drop-down list box. The default database is **default**.

   The system displays all available tables. You can enter a keyword of the table name to search for the desired table.

#. Click the desired table name. All columns in the table are displayed.

   Move the cursor to the row of the table and click |image2|. Column details are displayed.

#. In the SparkSql statement editing area, enter the query statement.

   Click the triangle next to |image3| and select **Explain**. The editor checks the syntax and execution plan of the entered statements. If the statements have syntax errors, the editor reports **Error while compiling statement**.

#. Click |image4| to execute the SparkSql statement.

   .. note::

      -  If you want to use the entered SparkSql statements again, click |image5| to save them.

      -  Advanced query configuration:

         Click |image6| in the upper right corner to configure information such as files, functions, and settings.

      -  Viewing the information of shortcut keys:

         Click |image7| in the upper right corner to view the syntax and keyboard shortcut information.

      -  To format the SparkSql statement, click the triangle next to |image8| and select **Format**.

      -  To delete an entered SparkSql statement, click the triangle next to |image9| and select **Clear**.

      -  Viewing historical records:

         Click **Query History** to view the SparkSql running status. You can view the history of all the statements or only the saved statements. If many historical records exist, you can enter keywords in the text box to search for desired records.

Viewing Execution Results
-------------------------

#. View the execution results below the execution area on **SparkSql**. The **Query History** tab page is displayed by default.
#. Click a result to view the execution result of the executed statement.

Managing Query Statements
-------------------------

#. Click **Saved Queries**.
#. Click a saved statement. The system automatically adds the statement to the editing area.

.. |image1| image:: /_static/images/en-us_image_0000001296090532.png
.. |image2| image:: /_static/images/en-us_image_0000001349289861.jpg
.. |image3| image:: /_static/images/en-us_image_0000001296090524.jpg
.. |image4| image:: /_static/images/en-us_image_0000001295770740.jpg
.. |image5| image:: /_static/images/en-us_image_0000001348770561.png
.. |image6| image:: /_static/images/en-us_image_0000001295930708.png
.. |image7| image:: /_static/images/en-us_image_0000001349090373.png
.. |image8| image:: /_static/images/en-us_image_0000001348770553.jpg
.. |image9| image:: /_static/images/en-us_image_0000001295770748.jpg
