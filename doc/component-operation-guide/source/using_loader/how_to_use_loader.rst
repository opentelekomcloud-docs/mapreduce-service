:original_name: mrs_01_0401.html

.. _mrs_01_0401:

How to Use Loader
=================

This section applies to MRS clusters earlier than 3.\ *x*.

Process
-------

The process for migrating user data with Loader is as follows:

#. Access the Loader page of the Hue web UI.
#. Manage Loader links.
#. Create a job and select a data source link and a link for saving data.
#. Run the job to complete data migration.

.. _mrs_01_0401__s12f4baccf3914471bee631d0ca198278:

Loader Page
-----------

The Loader page is a graphical data migration management tool based on the open source Sqoop web UI and is hosted on the Hue web UI. Perform the following operations to access the Loader page:

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0370>`.

#. Choose **Data Browsers** > **Sqoop**.

   The job management tab page is displayed by default on the Loader page.

Loader Links
------------

Loader links save data location information. Loader uses links to access data or save data to the specified location. Perform the following operations to access the Loader link management page:

#. Access the Loader page.

#. Click **Manage links**.

   The Loader link management page is displayed.

   Click **Manage jobs** to return to the job management page.

#. Click **New link** to go to the configuration page and set parameters to create a Loader link.

Loader Jobs
-----------

Loader jobs are used to manage data migration tasks. Each job consists of a source data link and a destination data link. A job reads data from the source link and saves data to the destination link to complete a data migration task.
