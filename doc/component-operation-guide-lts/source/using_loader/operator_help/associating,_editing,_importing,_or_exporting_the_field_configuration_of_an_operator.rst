:original_name: mrs_01_1152.html

.. _mrs_01_1152:

Associating, Editing, Importing, or Exporting the Field Configuration of an Operator
====================================================================================

Scenario
--------

This section describes how to associate, import, or export the field configuration information of an operator when creating or editing a Loader job.

-  Associating the field configuration of an operator

   Associate the field configuration information of an input operator with an output operator.

-  Editing the field configuration of an operator

   Edit the field configuration information of an operator.

-  Importing the field configuration of an operator

   Import the field configuration information to an operator by using an operator export file or operator template file.

-  Exporting the field configuration of an operator

   Export the field configuration information of an operator to a JSON file and save the file to a local directory.

Prerequisites
-------------

You have obtained the username and password for logging in to the Loader web UI.

Procedure
---------

-  **Associating Field Configuration of an Operator**

#. Access the Loader web UI.

   a. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.

   b. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader**.

   c. Click **LoaderServer(**\ *Node name*\ **, Active)**. The Loader web UI is displayed.


      .. figure:: /_static/images/en-us_image_0000001438241209.png
         :alt: **Figure 1** Loader web UI

         **Figure 1** Loader web UI

#. Edit an existing job or create a new job. The **Transform** page is displayed.
#. Double-click a specified input operator (such as **CSV File Input**) to go to the edit page. Add the configuration information to the parameter table of the input field.
#. Double-click a specified output operator (such as **File Output**) to go to the edit page, click **associate**, and select the required field information in the displayed **associate** dialog box.

   .. note::

      -  The field name already exists in the field table of the output operator and is not displayed in the **associate** window.
      -  You can also select the required field from the **field name** list. The corresponding configuration information is displayed in the parameter table of the output field.

#. Click **OK**. The selected field is displayed in the parameter table of the output field.

-  **Editing the Field Configuration of an Operator**

#. Access the Loader web UI.

   a. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.
   b. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader**.
   c. Click **LoaderServer(**\ *Node name*\ **, Active)**. The Loader web UI is displayed.

#. Edit an existing job or create a new job. The **Transform** page is displayed.

#. Double-click a specified operator (such as **CSV File Input**) to go to the edit page. On the **Table Edit** tab page of the input field, click **Add** and enter the field information based on the parameter requirements of the operator.

#. You can move (up or down), insert a row under, and delete a field by clicking buttons corresponding to the field.

   Click **Text Area Edit** to edit the field list in text format. Use commas (,) to separate field attributes.

   |image1|

#. Click **OK**.

-  **Importing the Field Configuration of an Operator**

#. Access the Loader web UI.

   a. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.
   b. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader**.
   c. Click **LoaderServer(**\ *Node name*\ **, Active)**. The Loader web UI is displayed.

#. Edit an existing job or create a new job. The **Transform** page is displayed.
#. Double-click a specified operator to go to the editing page and add related configuration information to the parameter table of the input or output field. Click **Import**.
#. Select an import type.

   -  Export File

      Field configuration information is imported by using the JSON file exported by the operator.

   -  Specified Template

      Field configuration information is imported by using the TXT file compiled based on the operator template.

#. Click |image2| and select the upload file path.
#. Click **Upload**. The field configuration information is imported to the operator.

-  **Exporting the Field Configuration of an Operator**

#. Access the Loader web UI.

   a. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.
   b. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Loader**.
   c. Click **LoaderServer(**\ *Node name*\ **, Active)**. The Loader web UI is displayed.

#. Edit an existing job or create a new job. The **Transform** page is displayed.
#. Double-click a specified operator to go to the editing page, add related configuration information to the parameter table of the input or output field, and click **Export**.
#. Select an export type.

   -  All

      All field information is exported as a JSON file and saved to a local directory.

   -  Specified Field Name

      Fields selected in the field list are exported as a JSON file and saved to a local directory.

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001349059569.png
.. |image2| image:: /_static/images/en-us_image_0000001296059724.png
