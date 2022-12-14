:original_name: mrs_01_1825.html

.. _mrs_01_1825:

Submitting a Sub-workflow Job
=============================

Scenario
--------

This section describes how to submit an Oozie job of the Sub-workflow type on the Hue web UI.

Procedure
---------

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. On the workflow editing page, select |image1| next to **Sub workflow** and drag it to the operation area.

#. In the **Sub workflow** dialog box that is displayed, set **Sub-workflow**, for example, to **Java-Workflow** (one of the created workflows) from the drop-down list box, and click **Add**.

   |image2|

#. Click |image3| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **Subworkflow-Workflow**.

#. After the configuration is saved, click |image4|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001349169829.jpg
.. |image2| image:: /_static/images/en-us_image_0000001296249732.png
.. |image3| image:: /_static/images/en-us_image_0000001295930260.png
.. |image4| image:: /_static/images/en-us_image_0000001295770304.jpg
