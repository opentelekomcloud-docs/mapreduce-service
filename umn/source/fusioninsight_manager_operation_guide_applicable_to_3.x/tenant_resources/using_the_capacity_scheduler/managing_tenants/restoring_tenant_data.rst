:original_name: admin_guide_000123.html

.. _admin_guide_000123:

Restoring Tenant Data
=====================

Scenario
--------

Tenant data is stored on FusionInsight Manager and cluster components. When components are recovered from failures or reinstalled, some configuration data of all tenants may become abnormal. In this case, you need to manually restore the configuration data on FusionInsight Manager.

Procedure
---------

#. Log in to FusionInsight Manager and choose **Tenant Resources**.

#. In the tenant list on the left, click the target tenant.

#. Check the tenant data status.

   a. On the **Summary** page, check **Tenant Status**. A green icon indicates that the tenant is available and gray indicates that the tenant is unavailable.
   b. Click **Resource** and check the icons on the left of **Yarn** and **HDFS Storage**. A green icon indicates that the resource is available, and gray indicates that the resource is unavailable.
   c. Click **Service Associations** and check the **Status** column of the associated services. **Normal** indicates that the component can provide services for the associated tenant. **Not Available** indicates that the component cannot provide services for the tenant.
   d. If any of the preceding check items is abnormal, go to :ref:`4 <admin_guide_000123__l62f85b027a17495484c1162c5dd730f1>` to restore tenant data.

#. .. _admin_guide_000123__l62f85b027a17495484c1162c5dd730f1:

   Click |image1|. In the displayed dialog box, enter the password of the current login user and click **OK**.

#. In the **Restore Tenant Resource Data** window, select one or more components to restore data, and click **OK**. The system automatically restores the tenant data.

.. |image1| image:: /_static/images/en-us_image_0263899446.png
