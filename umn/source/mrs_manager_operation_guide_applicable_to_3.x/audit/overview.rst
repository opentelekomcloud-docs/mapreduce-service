:original_name: admin_guide_000085.html

.. _admin_guide_000085:

Overview
========

Scenario
--------

The **Audit** page displays the user operations on Manager. On this page, administrators can view historical user operations on Manager. For details about the audit information, see :ref:`Audit Logs <admin_guide_000193__s481f1c14aca34ee788baed345970a5c0>`.


Overview
--------

Log in to MRS Manager and choose **Audit**. The **Audit** page displays the operation type, risk level, start time, end time, user, source, host name, service, instance, and operation result.

-  You can select audit logs at the **Critical**, **Major**, **Minor**, or **Notice** level from the **All risk levels** drop-down list.
-  In **Advanced Search**, you can set filter criteria to query audit logs.

   #. You can query audit logs by user management, cluster, service, and health in the **Operation Type** column.
   #. In the **Service** column, you can select a service to query corresponding audit logs.

      .. note::

         You can select **--** to search for audit logs using all other search criteria except services.

   #. You can query audit logs by operation result. Value options are **All**, **Successful**, **Failed**, and **Unknown**.

-  You can click |image1| to manually refresh the current page or click |image2| to filter the columns displayed in the page.
-  Click **Export All** to export all audit information at a time. The audit information can be exported in **TXT** or **CSV** format.

.. |image1| image:: /_static/images/en-us_image_0000001442494041.png
.. |image2| image:: /_static/images/en-us_image_0000001442413865.png
