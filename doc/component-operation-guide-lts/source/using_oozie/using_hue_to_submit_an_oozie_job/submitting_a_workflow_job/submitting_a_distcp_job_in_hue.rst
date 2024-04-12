:original_name: mrs_01_1829.html

.. _mrs_01_1829:

Submitting a DistCp Job in Hue
==============================

Scenario
--------

This section describes how to submit an Oozie job of the DistCp type on the Hue web UI.

Procedure
---------

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. On the workflow editing page, select |image1| next to **Distcp** and drag it to the operation area.

#. Determine whether the current DistCp operation is performed across clusters.

   -  If yes, go to :ref:`4 <mrs_01_1829__en-us_topic_0000001173630708_li15967531204920>`.
   -  If no, go to :ref:`7 <mrs_01_1829__en-us_topic_0000001173630708_le4a671e8c2a94b948e244fe188cfe08f>`.

#. .. _mrs_01_1829__en-us_topic_0000001173630708_li15967531204920:

   Establish cross-Manager mutual trust between two clusters.

#. In the **Distcp** window that is displayed, set the value of **Source**, for example, to **hdfs://hacluster/user/admin/examples/input-data/text/data.txt**. Set **Destination**, for example, to **hdfs://target_ip:target_port/user/admin/examples/output-data/distcp-workflow/data.txt**. Click **Add**.

#. Click the configuration button |image2| in the upper right corner. On the **Properties** tab page, click **PROPERTIES+**, enter the attribute name **oozie.launcher.mapreduce.job.hdfs-servers** in the text box on the left, enter the attribute value **hdfs://**\ *source_ip:source_port*\ **,hdfs://**\ *target_ip:target_port* in the text box on the right, and go to :ref:`8 <mrs_01_1829__en-us_topic_0000001173630708_lfc85380934e241ed8783edbf9b9a4e0f>`.

   .. note::

      *source_ip*: service address of the HDFS NameNode in the source cluster

      *source_port*: port number of the HDFS NameNode in the source cluster.

      *target_ip*: service address of the HDFS NameNode in the target cluster

      *target_port*: port number of the HDFS NameNode in the target cluster.

#. .. _mrs_01_1829__en-us_topic_0000001173630708_le4a671e8c2a94b948e244fe188cfe08f:

   In the **Distcp** window that is displayed, set the value of **Source**, for example, to **/user/admin/examples/input-data/text/data.txt**. Set **Destination**, for example, to **/user/admin/examples/output-data/distcp-workflow/data.txt**. Click **Add**.

#. .. _mrs_01_1829__en-us_topic_0000001173630708_lfc85380934e241ed8783edbf9b9a4e0f:

   Click |image3| in the upper right corner. On the configuration page that is displayed, click **Delete+** and add the directory to be deleted, for example, **/user/admin/examples/output-data/distcp-workflow**.

#. Click |image4| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **Distcp-Workflow**.

#. After the configuration is saved, click |image5|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001349259217.jpg
.. |image2| image:: /_static/images/en-us_image_0000001349259213.jpg
.. |image3| image:: /_static/images/en-us_image_0000001348739937.jpg
.. |image4| image:: /_static/images/en-us_image_0000001295740104.png
.. |image5| image:: /_static/images/en-us_image_0000001348739933.jpg
