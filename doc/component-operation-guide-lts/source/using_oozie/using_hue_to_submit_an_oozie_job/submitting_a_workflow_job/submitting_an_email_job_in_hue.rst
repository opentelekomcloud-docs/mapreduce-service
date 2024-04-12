:original_name: mrs_01_24114.html

.. _mrs_01_24114:

Submitting an Email Job in Hue
==============================

Scenario
--------

This section describes how to add an email job on the Hue web UI.

Procedure
---------

#. Log in to Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Oozie** > **Configurations**, switch from **Basic Configurations** to **All Configurations**, and search for the **oozie.site.configs** parameter.

   |image1|

#. Add the following parameters and click **Save**. In the displayed dialog box, click **OK**.

   .. table:: **Table 1** Parameters

      +--------------------------------+-------------------------------------------------------------+
      | Name                           | Value                                                       |
      +================================+=============================================================+
      | oozie.email.smtp.host          | *SMTP server*, for example, **xxx.xxx.com**.                |
      +--------------------------------+-------------------------------------------------------------+
      | oozie.email.from.address       | *Sender email address*, for example, **zhangsan@\ xx.com**. |
      +--------------------------------+-------------------------------------------------------------+
      | oozie.email.smtp.auth          | **true**                                                    |
      +--------------------------------+-------------------------------------------------------------+
      | oozie.email.smtp.username      | *Sender account*, for example, **zhangsan**.                |
      +--------------------------------+-------------------------------------------------------------+
      | oozie.email.smtp.password      | *Sender account password*, for example, **111111**.         |
      +--------------------------------+-------------------------------------------------------------+
      | oozie.email.attachment.enabled | **true**                                                    |
      +--------------------------------+-------------------------------------------------------------+
      | oozie.email.smtp.port          | *SMTP server port number*, for example, **25**.             |
      +--------------------------------+-------------------------------------------------------------+

#. On the Oozie dashboard page, choose **More** > **Restart Service**, enter the system administrator password, and click **OK** to restart the Oozie service.

#. Log in to the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

#. In the navigation tree on the left, click |image2| and choose **Workflow** to open the Workflow editor.

#. Click **Documents**, click |image3| to select a Hive script from the operation list, and drag it to the operation page.

   |image4|

#. In the displayed dialog box, configure **To addresses**, **Subject**, and **Body**, and click **Add**.

   -  **To addresses**: specifies the recipient email address. Separate multiple email addresses with commas (,).
   -  **Subject**: specifies the email subject.
   -  **Body**: specifies the email body.

#. You can configure **cc**, **bcc**, and **Attachment** in the displayed dialog box based on service requirements.

   -  **cc**: specifies the address that will receive the carbon copy of the email. Separate multiple email addresses with commas (,).
   -  **bcc**: specifies the address that will receive the carbon copy of the email and is invisible to the recipient. Separate multiple email addresses with commas (,).
   -  **Attachment**: specifies the HDFS address of the attachment.

   |image5|

#. Click |image6| in the upper right corner of the Oozie editor to save the job.

#. After the job is saved, click |image7|. In the displayed dialog box, click **Submit** to submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on the Hue web UI.

.. |image1| image:: /_static/images/en-us_image_0000001296219420.png
.. |image2| image:: /_static/images/en-us_image_0000001349139501.png
.. |image3| image:: /_static/images/en-us_image_0000001296059792.png
.. |image4| image:: /_static/images/en-us_image_0000001295739984.png
.. |image5| image:: /_static/images/en-us_image_0000001348739813.png
.. |image6| image:: /_static/images/en-us_image_0000001295739980.png
.. |image7| image:: /_static/images/en-us_image_0000001296059788.jpg
