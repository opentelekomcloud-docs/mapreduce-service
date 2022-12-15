:original_name: alm_14003.html

.. _alm_14003:

ALM-14003 Number of Lost HDFS Blocks Exceeds the Threshold
==========================================================

Description
-----------

The system checks the number of lost blocks every 30 seconds and compares the number of lost blocks with the threshold. The lost blocks indicator has a default threshold. This alarm is generated when the number of lost blocks exceeds the threshold.

This alarm is cleared when the number of lost blocks is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14003    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------------------+
| Parameter         | Description                                                                         |
+===================+=====================================================================================+
| ServiceName       | Specifies the service for which the alarm is generated.                             |
+-------------------+-------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| NSName            | Specifies the NameService service for which the alarm is generated.                 |
+-------------------+-------------------------------------------------------------------------------------+
| Trigger condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

Data stored in HDFS is lost. HDFS may enter the safe mode and cannot provide write services. Lost block data cannot be restored.

Possible Causes
---------------

-  The DataNode instance is abnormal.
-  Data is deleted.

Procedure
---------

#. Check the DataNode instance.

   a. On the MRS cluster details page, choose **Components** > **HDFS** > **Instances**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and choose **Services** > **HDFS** > **Instances**.

   b. Check whether the status of all DataNode instances is **Good**.

      -  If yes, go to :ref:`3 <alm_14003__en-us_topic_0191813959_li572522141314>`.
      -  If no, go to :ref:`1.c <alm_14003__en-us_topic_0191813959_li2677020115402>`.

   c. .. _alm_14003__en-us_topic_0191813959_li2677020115402:

      Restart the DataNode instance and check whether the restart is successful.

      -  If yes, go to :ref:`2.b <alm_14003__en-us_topic_0191813959_li4975462315402>`.
      -  If no, go to :ref:`2.a <alm_14003__en-us_topic_0191813959_li435173115402>`.

#. Delete the damaged file.

   a. .. _alm_14003__en-us_topic_0191813959_li435173115402:

      Use the client on the cluster node. Run the **hdfs fsck / -delete** command to delete the lost file. Then rewrite the file and recover the data.

   b. .. _alm_14003__en-us_topic_0191813959_li4975462315402:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_14003__en-us_topic_0191813959_li572522141314>`.

#. .. _alm_14003__en-us_topic_0191813959_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
