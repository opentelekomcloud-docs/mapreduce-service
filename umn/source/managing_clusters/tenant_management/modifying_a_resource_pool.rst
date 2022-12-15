:original_name: mrs_01_0311.html

.. _mrs_01_0311:

Modifying a Resource Pool
=========================

Scenario
--------

You can modify members of an existing resource pool on MRS.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS details page, click **Tenants**.

   .. note::

      For MRS 1.7.2 or earlier, see :ref:`Modifying a Resource Pool <mrs_01_0545>`. For MRS 3.x or later, see :ref:`Overview <admin_guide_000097>`.

#. Click the **Resource Pools** tab.
#. Locate the row that contains the specified resource pool, and click **Modify** in the **Operation** column.
#. In **Modify Resource Pool**, modify **Added Hosts**.

   -  Adding a host: In the host list on the left, select the specified host name and add it to the resource pool.
   -  Deleting a host: In the host list on the right, click |image1| next to a host to remove the host from the resource pool. The host list of a resource pool can be left blank.

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001349057681.png
