:original_name: mrs_01_2363.html

.. _mrs_01_2363:

Configuring a Hudi Data Source
==============================

Scenario
--------

HetuEngine can be connected to the Hudi data source of the cluster of MRS 3.1.1 or later.

.. note::

   HetuEngine does not support the reading of Hudi bootstrap tables.

Prerequisites
-------------

-  You have created the proxy user of the Hudi data source. The proxy user is a human-machine user and must belong to the **hive** group.
-  You have created a HetuEngine administrator by referring to :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Procedure
---------

#. Perform :ref:`1 <mrs_01_2348__en-us_topic_0000001219351171_li4515762384>` to :ref:`6.g <mrs_01_2348__en-us_topic_0000001219351171_li1438274211549>` to configure a traditional data source by referring to :ref:`Configuring a Traditional Data Source <mrs_01_2348>`.

#. In the **Custom Configuration** area, add a custom parameter, as listed in :ref:`Table 1 <mrs_01_2363__en-us_topic_0000001219149163_table1687934216313>`.

   .. _mrs_01_2363__en-us_topic_0000001219149163_table1687934216313:

   .. table:: **Table 1** Custom configuration parameter for Hudi data

      ============================= =====
      Custom Parameter Name         Value
      ============================= =====
      hive.parquet.use-column-names true
      ============================= =====

#. Click **OK**.
