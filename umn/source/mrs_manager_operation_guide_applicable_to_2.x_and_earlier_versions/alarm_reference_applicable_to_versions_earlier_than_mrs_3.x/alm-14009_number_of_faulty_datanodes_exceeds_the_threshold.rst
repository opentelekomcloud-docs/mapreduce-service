:original_name: alm_14009.html

.. _alm_14009:

ALM-14009 Number of Faulty DataNodes Exceeds the Threshold
==========================================================

Description
-----------

The system periodically checks the number of faulty DataNodes in the HDFS cluster every 30 seconds, and compares the number with the threshold. The number of faulty DataNodes has a default threshold. This alarm is generated when the number of faulty DataNodes in the HDFS cluster exceeds the threshold.

This alarm is cleared when the number of faulty DataNodes in the HDFS cluster is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14009    Major          Yes
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
| Trigger condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

Faulty DataNodes cannot provide HDFS services.

Possible Causes
---------------

-  DataNodes are faulty or overloaded.
-  The network between the NameNode and the DataNode is disconnected or busy.
-  NameNodes are overloaded.

Procedure
---------

#. Check whether DataNodes are faulty.

   a. Use the client on the cluster node and run the **hdfs dfsadmin -report** command to check whether DataNodes are faulty.

      -  If yes, go to :ref:`1.b <alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step4>`.
      -  If no, go to :ref:`2.a <alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step6>`.

   b. .. _alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step4:

      On the MRS cluster details page, choose **Components** > **HDFS** > **Instances** to check whether the DataNode is stopped.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and choose **Services** > **HDFS** > **Instances**.

      -  If yes, go to :ref:`1.c <alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step5>`.
      -  If no, go to :ref:`2.a <alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step6>`.

   c. .. _alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step5:

      Select the DataNode instance, and choose **More** > **Restart Instance** to restart it. Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step6>`.

#. Check the status of the network between the NameNode and the DataNode.

   a. .. _alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step6:

      Log in to the service IP address of the node where the faulty DataNode is located, and run the **ping** *IP address of the NameNode* command to check whether the network between the DataNode and the NameNode is abnormal.

      -  If yes, go to :ref:`2.b <alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step7>`.
      -  If no, go to :ref:`3.a <alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step8>`.

   b. .. _alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step7:

      Rectify the network fault. Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3.a <alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step8>`.

#. Check whether the DataNode is overloaded.

   a. .. _alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step8:

      On the MRS cluster details page, click **Alarms** and check whether the alarm ALM-14008 HDFS DataNode Memory Usage Exceeds the Threshold exists.

      -  If yes, go to :ref:`3.b <alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step13>`.
      -  If no, go to :ref:`4.a <alm_14009__en-us_topic_0191813881_step9>`.

   b. .. _alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step13:

      Follow procedures in :ref:`ALM-14008 HDFS DataNode Memory Usage Exceeds the Threshold <alm_14008>` to handle the alarm and check whether the alarm is cleared.

      -  If yes, go to :ref:`3.c <alm_14009__en-us_topic_0191813881_ss10>`.
      -  If no, go to :ref:`4.a <alm_14009__en-us_topic_0191813881_step9>`.

   c. .. _alm_14009__en-us_topic_0191813881_ss10:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4.a <alm_14009__en-us_topic_0191813881_step9>`.

#. Check whether the NameNode is overloaded.

   a. .. _alm_14009__en-us_topic_0191813881_step9:

      On the MRS cluster details page, click **Alarms** and check whether the alarm ALM-14007 HDFS NameNode Memory Usage Exceeds the Threshold exists.

      -  If yes, go to :ref:`4.b <alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step14>`.
      -  If no, go to :ref:`5 <alm_14009__en-us_topic_0191813881_li572522141314>`.

   b. .. _alm_14009__en-us_topic_0191813881_alm14007_3_mmccppss_step14:

      Follow procedures in :ref:`ALM-14007 HDFS NameNode Memory Usage Exceeds the Threshold <alm_14007>` to handle the alarm and check whether the alarm is cleared.

      -  If yes, go to :ref:`4.c <alm_14009__en-us_topic_0191813881_ss13>`.
      -  If no, go to :ref:`5 <alm_14009__en-us_topic_0191813881_li572522141314>`.

   c. .. _alm_14009__en-us_topic_0191813881_ss13:

      Wait 5 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`5 <alm_14009__en-us_topic_0191813881_li572522141314>`.

#. .. _alm_14009__en-us_topic_0191813881_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
