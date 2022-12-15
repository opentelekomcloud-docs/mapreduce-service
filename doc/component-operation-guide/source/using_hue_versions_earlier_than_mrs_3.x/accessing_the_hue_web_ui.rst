:original_name: mrs_01_0370.html

.. _mrs_01_0370:

Accessing the Hue Web UI
========================

Scenario
--------

After Hue is installed in an MRS cluster, users can use Hadoop and Hive on the Hue web UI.

For versions earlier than MRS 1.9.2, MRS clusters with Kerberos authentication enabled support this function.

This section describes how to open the Hue web UI on the MRS cluster.

.. note::

   To access the Hue web UI, you are advised to use a browser that is compatible with the Hue WebUI, for example, Google Chrome 50. The Internet Explorer may be incompatible with the Hue web UI.

   For versions earlier than MRS 1.9.2, the Kerberos authentication is disabled for an MRS cluster, access the Hue web UI by referring to `Web UIs of Open Source Components <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0362.html>`__.

Impact on the System
--------------------

Site trust must be added to the browser when you access Manager and Hue web UI for the first time. Otherwise, the Hue web UI cannot be accessed.

Prerequisites
-------------

When Kerberos authentication is enabled, the MRS cluster administrator has assigned the permission for using Hive to the user. For details, see `Creating a User <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0345.html>`__. For example, create a human-machine user named **hueuser**, add the user to user groups **hive** (the primary group), **hadoop**, and **supergroup**, and role **System_administrator**.

This user is used to log in to the Hue WebUI.

Procedure
---------

#. Log in to the service page.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services**.
   -  For MRS 1.9.2 or later, click the cluster name on the MRS console and choose **Components**.

#. Select **Hue**. On the right side of **Hue WebUI**, click the link to log in to the Hue web UI as user **hueuser**.

   Hue WebUI provides the following functions:

   -  If Hive is installed in the MRS cluster, you can use **Query Editors** to execute query statements of Hive. Hive has been installed in the MRS cluster.
   -  If Hive is installed in the MRS cluster, you can use **Data Browsers** to manage Hive tables.
   -  If HDFS is installed in the MRS cluster, you can use |image1| to view directories and files in HDFS.
   -  If Yarn is installed in the MRS cluster, you can use |image2| to view all jobs in the MRS cluster.

   .. note::

      -  When you log in to the Hue web UI as user **hueuser** for the first time, you need to change the password.
      -  After obtaining the URL for accessing the Hue web UI, you can give the URL to other users who cannot access MRS Manager for accessing the Hue web UI.
      -  If you perform operations on the Hue WebUI only but not on Manager, you must enter the password of the current login user when accessing Manager again.

.. |image1| image:: /_static/images/en-us_image_0000001349289509.png
.. |image2| image:: /_static/images/en-us_image_0000001349169933.png
