:original_name: ALM-13006.html

.. _ALM-13006:

ALM-13006 Znode Number or Capacity Exceeds the Threshold
========================================================

Description
-----------

The system periodically detects the status of secondary Znode in the ZooKeeper service data directory every four hours. This alarm is generated when the number or capacity of secondary Znodes exceeds the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
13006    Minor          Yes
======== ============== =====================

Parameters
----------

+-------------------+--------------------------------------------------------------+
| Name              | Meaning                                                      |
+===================+==============================================================+
| Source            | Specifies the cluster for which the alarm is generated.      |
+-------------------+--------------------------------------------------------------+
| ServiceName       | Specifies the service name for which the alarm is generated. |
+-------------------+--------------------------------------------------------------+
| ServiceDirectory  | Specifies the directory for which the alarm is generated.    |
+-------------------+--------------------------------------------------------------+
| Trigger Condition | Specifies the cause of the alarm.                            |
+-------------------+--------------------------------------------------------------+

Impact on the System
--------------------

A large amount of data is written to the ZooKeeper data directory. As a result, ZooKeeper cannot provide normal services.

Possible Causes
---------------

A large amount of data is written to the ZooKeeper data directory. The threshold is not appropriate.

Procedure
---------

**Check whether a large amount of data is written to the directory for which the alarm is generated.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. On the displayed interface, click the drop-down button of **Znode Number or Capacity Exceeds the Threshold**. Confirm the Znode for which the alarm is generated in Location Information.

#. Log in to MRS Manager, open the ZooKeeper service interface, and select **Resource**. In the table **Used Resources (By Second-Level Znode)**, check whether a large amount of data is written to the top-level Znode for which the alarm is reported.

   -  If it is, go to :ref:`3 <alm-13006__li47651981813>`.
   -  If it is not, go to :ref:`4 <alm-13006__li3567539141610>`.

#. .. _alm-13006__li47651981813:

   Log in to the ZooKeeper client and delete the data in the top-level Znode.

#. .. _alm-13006__li3567539141610:

   Log in to MRS Manager and open the ZooKeeper service interface. On the **Resource** page, choose |image1| > **By Znode quantity** in **Used Resources (By Second-Level Znode)**. **Threshold** **Configuration of By Znode quantity** is displayed. Click **Modify** under **Operation**. Increase the threshold by referringto the value of **max.Znode.count** by choosing **Cluster >** *Name of the desired cluster* **> Services** > **ZooKeeper** > **Configurations > All Configurations** **> Quota**.

#. In the **Used Resources (By Second-Level Znode)**, choose |image2| > **By capacity**. The **Threshold Settings** page of **By Capacity** is displayed. Click **Modify** under **Operation**. Increase the threshold by referring to the value of **max.data.size** by choosing **Cluster >** *Name of the desired cluster* **> Services** > **ZooKeeper** > **Configurations > All Configurations** > **Quota**.

#. Check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`7 <alm-13006__li27634817118>`.

**Collect fault information.**

7.  .. _alm-13006__li27634817118:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

8.  Select **ZooKeeper** in the required cluster from the **Service**.

9.  Click |image3| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000002278171933.png
.. |image2| image:: /_static/images/en-us_image_0000002278292689.png
.. |image3| image:: /_static/images/en-us_image_0000001583087513.png
