:original_name: mrs_01_24013.html

.. _mrs_01_24013:

Using Yonghong BI to Access HetuEngine
======================================

Prerequisites
-------------

-  Yonghong BI has been installed.
-  The JDBC JAR file has been obtained. For details, see :ref:`1 <mrs_01_2337__li599475416716>`.
-  A human-machine user has been created in the cluster. For details about how to create a user, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Procedure
---------

#. Open Yonghong Desktop and choose **Create Connection** > **presto**.

   |image1|

#. On the data source configuration page, set parameters by referring to :ref:`Figure 1 <mrs_01_24013__en-us_topic_0000001219231283_fig171919211236>`. **User** and **Password** are the username and password of the created human-machine user. After the configuration is complete, click **Test Connection**.

   .. _mrs_01_24013__en-us_topic_0000001219231283_fig171919211236:

   .. figure:: /_static/images/en-us_image_0000001295740208.png
      :alt: **Figure 1** Configuring the data source

      **Figure 1** Configuring the data source

   -  **Driver**: Choose **Custom** > **Select Custom Driver**. Click |image2|, edit the driver name, click **Upload File** to upload the obtained JDBC JAR file, and click **OK**.

      |image3|

   -  **URL**: For details, see "URL format" in :ref:`2 <mrs_01_24010__en-us_topic_0000001173789310_li6197135010379>`.

   -  **Server Login**: Select **Username and Password** and enter the username and password.

#. .. _mrs_01_24013__en-us_topic_0000001219231283_li55331456256:

   Click **New Data Set**. On the displayed page, change the save path by referring to :ref:`Figure 2 <mrs_01_24013__en-us_topic_0000001219231283_fig10932125853718>` and click **OK**.

   .. _mrs_01_24013__en-us_topic_0000001219231283_fig10932125853718:

   .. figure:: /_static/images/en-us_image_0000001295900172.png
      :alt: **Figure 2** Changing a path

      **Figure 2** Changing a path

#. In the connection area, select **hetu** > **hive** > **default** > **Views**. In the **New Data Set** area on the right, select **SQL Data Set**.

   |image4|

#. In the **Connection** area, select the new data set created in :ref:`3 <mrs_01_24013__en-us_topic_0000001219231283_li55331456256>`. All table information is displayed. Select a table, for example, **test**, and click **Refresh Data**. All table information is displayed in the **Data Details** area on the right.

   |image5|

.. |image1| image:: /_static/images/en-us_image_0000001440850393.png
.. |image2| image:: /_static/images/en-us_image_0000001349139725.jpg
.. |image3| image:: /_static/images/en-us_image_0000001440970317.png
.. |image4| image:: /_static/images/en-us_image_0000001349259309.png
.. |image5| image:: /_static/images/en-us_image_0000001349059857.png
