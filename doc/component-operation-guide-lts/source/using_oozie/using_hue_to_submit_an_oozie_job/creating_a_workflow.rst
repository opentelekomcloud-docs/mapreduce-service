:original_name: mrs_01_1818.html

.. _mrs_01_1818:

Creating a Workflow
===================

Scenario
--------

You can submit an Oozie job on the Hue management page, but a workflow must be created before the job is submitted.

Prerequisites
-------------

Before using Hue to submit an Oozie job, configure the Oozie client and upload the sample configuration file and JAR file to the specified HDFS directory. For details, see :ref:`Using the Oozie Client <mrs_01_1810>`.

Procedure
---------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

#. In the navigation tree on the left, click |image1| and choose **Workflow** to open the Workflow editor.

#. Select **Actions** from the **DOCUMENTS** drop-down list, select the job type to be created and drag it to the operation area.

   For submitting different job types, follow instructions in the following sections:

   -  :ref:`Submitting a Hive2 Job in Hue <mrs_01_1820>`
   -  :ref:`Submitting a Spark2x Job in Hue <mrs_01_1821>`
   -  :ref:`Submitting a Java Job in Hue <mrs_01_1822>`
   -  :ref:`Submitting a Loader Job in Hue <mrs_01_1823>`
   -  :ref:`Submitting a MapReduce Job in Hue <mrs_01_1824>`
   -  :ref:`Submitting a Sub-workflow Job in Hue <mrs_01_1825>`
   -  :ref:`Submitting a Shell Job in Hue <mrs_01_1826>`
   -  :ref:`Submitting an HDFS Job in Hue <mrs_01_1827>`
   -  :ref:`Submitting a DistCp Job in Hue <mrs_01_1829>`

.. |image1| image:: /_static/images/en-us_image_0000001296059856.png
