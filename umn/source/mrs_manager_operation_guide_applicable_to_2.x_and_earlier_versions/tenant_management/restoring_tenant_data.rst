:original_name: mrs_01_0543.html

.. _mrs_01_0543:

Restoring Tenant Data
=====================

Scenario
--------

Tenant data is stored on Manager and in cluster components by default. When components are restored from faults or reinstalled, some tenant configuration data may be abnormal. In this case, you can manually restore the tenant data.

Procedure
---------

#. On MRS Manager, click **Tenant**.

#. In the tenant list on the left, click a tenant node.

#. Check the status of the tenant data.

   a. In **Summary**, check the color of the circle on the left of **Basic Information**. Green indicates that the tenant is available and gray indicates that the tenant is unavailable.
   b. Click **Resources** and check the circle on the left of **Yarn** or **HDFS Storage**. Green indicates that the resource is available, and gray indicates that the resource is unavailable.
   c. Click **Service Association** and check the **Status** column of the associated service table. **Good** indicates that the component can provide services for the associated tenant. **Bad** indicates that the component cannot provide services for the tenant.
   d. If any check result is abnormal, go to :ref:`4 <mrs_01_0543__en-us_topic_0035271545_li10849798195335>` to restore tenant data.

#. .. _mrs_01_0543__en-us_topic_0035271545_li10849798195335:

   Click **Restore Tenant Data**.

#. In the **Restore Tenant Data** window, select one or more components whose data needs to be restored. Click **OK**. The system automatically restores the tenant data.
