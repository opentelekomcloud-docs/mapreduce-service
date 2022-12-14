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

#. .. _mrs_01_1818__li1028081585415:

   Prepare a user who has operation permissions on the corresponding components.

   For example, log in to FusionInsight Manager as user **admin** and choose **System** in the top menu bar. On the **System** page that is displayed, choose **User** under **Permission** in the navigation pane on the left. On the displayed **User** page, click **Create**. On the **Create** page, set **Username** to **hueuser** and **User Type** to **Human-Machine**, set the password and confirm it, set **User Group** to **hive**, **hadoop**, and **supergroup**, set **Primary Group** to **hive**, set **Role** to **System_administrator**, and click **OK**.

#. Log in to FusionInsight Manager as the user created in :ref:`1 <mrs_01_1818__li1028081585415>` (change the password upon your first login), choose **Cluster** > **Services** > **Hue**, and click the link next to **Hue WebUI** to go to the Hue WebUI page.

#. In the navigation tree on the left, click |image1| and choose **Workflow** to open the Workflow editor.

#. Select **Actions** from the **DOCUMENTS** drop-down list, select the job type to be created and drag it to the operation area.

   |image2|

   For submitting different job types, follow instructions in the following sections:

   -  :ref:`Submitting a Hive2 Job <mrs_01_1820>`
   -  :ref:`Submitting a Spark2x Job <mrs_01_1821>`
   -  :ref:`Submitting a Java Job <mrs_01_1822>`
   -  :ref:`Submitting a Loader Job <mrs_01_1823>`
   -  :ref:`Submitting a MapReduce Job <mrs_01_1824>`
   -  :ref:`Submitting a Sub-workflow Job <mrs_01_1825>`
   -  :ref:`Submitting a Shell Job <mrs_01_1826>`
   -  :ref:`Submitting an HDFS Job <mrs_01_1827>`
   -  :ref:`Submitting a Streaming Job <mrs_01_1828>`
   -  :ref:`Submitting a DistCp Job <mrs_01_1829>`

.. |image1| image:: /_static/images/en-us_image_0000001295930388.png
.. |image2| image:: /_static/images/en-us_image_0000001295770428.png
