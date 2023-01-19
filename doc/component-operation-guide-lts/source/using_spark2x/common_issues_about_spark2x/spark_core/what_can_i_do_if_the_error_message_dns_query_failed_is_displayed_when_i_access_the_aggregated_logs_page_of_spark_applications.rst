:original_name: mrs_01_2015.html

.. _mrs_01_2015:

What Can I Do If the Error Message "DNS query failed" Is Displayed When I Access the Aggregated Logs Page of Spark Applications?
================================================================================================================================

Question
--------

When the **http(s)://<spark ip>:<spark port>** mode is used to access the Spark JobHistory page, if the displayed Spark JobHistory page is not the page of FusionInsight Manager (the URL of FusionInsight Manager is similar to **https://<oms ip>:20026/Spark2x/JobHistory2x/xx/**), click an application and click **AggregatedLogs**, click the logs of an executor to be viewed. An error message in :ref:`Figure 1 <mrs_01_2015__en-us_topic_0000001219231305_fa5532996a7a74910b0d8a19be7ffc2c0>` is displayed.

.. _mrs_01_2015__en-us_topic_0000001219231305_fa5532996a7a74910b0d8a19be7ffc2c0:

.. figure:: /_static/images/en-us_image_0000001389312782.png
   :alt: **Figure 1** DNS query failure

   **Figure 1** DNS query failure

Answer
------

**Cause**: The domain name is not added to the **hosts** file of the Windows OS in the pop-up URL (for example, **https://<hostname>:20026/Spark2x/JobHistory2x/xx/history/application_xxx/jobs/**). As a result, the DNS query fails and the web page cannot be displayed.

**Solution:**

-  You are advised to visit **Spark JobHistory** page using the FusionInsight Manager. Click the links in the blue box in :ref:`Figure 2 <mrs_01_2015__en-us_topic_0000001219231305_f4748f8aec3164955b2d8942bee9ddef3>`.

   .. _mrs_01_2015__en-us_topic_0000001219231305_f4748f8aec3164955b2d8942bee9ddef3:

   .. figure:: /_static/images/en-us_image_0000001389632602.png
      :alt: **Figure 2** Spark2x page of FusionInsight Manager

      **Figure 2** Spark2x page of FusionInsight Manager

-  If you do not want to access the **Spark JobHistory** page using the FusionInsight Manager, change **<hostname>** in the URL to the IP address or add the domain name to the **hosts** file of the Windows OS.
