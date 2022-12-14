:original_name: mrs_01_2340.html

.. _mrs_01_2340:

Why Do I Fail to Create a Table in the Specified Location on OBS After Logging to spark-beeline?
================================================================================================

Question
--------

When the OBS ECS/BMS image cluster is connected, after spark-beeline is logged in, an error is reported when a location is specified to create a table on OBS.


.. figure:: /_static/images/en-us_image_0000001349090021.png
   :alt: **Figure 1** Error message

   **Figure 1** Error message

Answer
------

The permission on the **ssl.jceks** file in HDFS is insufficient. As a result, the table fails to be created.

|image1|

Solution
--------

#. Log in to the node where Spark2x resides as user **omm** and run the following command:

   **vi ${BIGDATA_HOME}/FusionInsight_Spark2x\_8.1.0.1/install/FusionInsight-Spark2x-3.1.1/spark/sbin/fake_prestart.sh**

#. Change **eval "${hdfsCmd}" -chmod 600 "${InnerHdfsDir}"/ssl.jceks >> "${PRESTART_LOG}" 2>&1** to **eval "${hdfsCmd}" -chmod 644 "${InnerHdfsDir}"/ssl.jceks >> "${PRESTART_LOG}" 2>&1**.

#. Restart the SparkResource instance.

.. |image1| image:: /_static/images/en-us_image_0000001387912132.png
