:original_name: mrs_01_2044.html

.. _mrs_01_2044:

Why Are Some Functions Not Available when Another JDBCServer Is Connected?
==========================================================================

Question
--------

Scenario 1

I set up permanent functions using the **add jar** statement. After Beeline connects to different JDBCServer or  JDBCServer is restarted, I have to run the **add jar** statement again.


.. figure:: /_static/images/en-us_image_0000001438709421.png
   :alt: **Figure 1** Error information in scenario 1

   **Figure 1** Error information in scenario 1

Scenario 2

The **show functions** statement can be used to query functions, but not obtain functions. The reason is that connected JDBC node does not contain jar packages of the corresponding path. However, after I add corresponding **.jar** packages, the **show functions** statement can be used to obtain functions.


.. figure:: /_static/images/en-us_image_0000001349170953.png
   :alt: **Figure 2** Error information in scenario 2

   **Figure 2** Error information in scenario 2

Answer
------

Scenario 1

The **add jar** statement is used to load jars to the jarClassLoader of the JDBCServer connected currently. The **add jar** statement is not shared by different JDBCServer. After the JDBCServer restarts, new jarClassLoader is created. So the add jar statement needs to be run again.

There are two methods to add jar packages: You can run the **spark-sql --jars /opt/test/two_udfs.jar** statement to add the jar package during the startup of the Spark SQL process; or run the **add jar /opt/test/two_udfs.jar** statement to add the jar package after the Spark SQL process is started. Note that the path following the add jar statement can be a local path or an HDFS path.

Scenario 2

The show functions statement is used to obtain all functions in the current database from the external catalog. If functions are used in SQL, thriftJDBC-server loads **.jar** files related to the function.

If **.jar** files do not exist, the function cannot obtain corresponding **.jar** files. Therefore, the corresponding **.jar** files need to be added.
