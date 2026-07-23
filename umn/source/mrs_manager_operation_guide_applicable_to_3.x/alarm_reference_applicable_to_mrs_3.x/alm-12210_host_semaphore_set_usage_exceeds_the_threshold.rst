:original_name: ALM-12210.html

.. _ALM-12210:

ALM-12210 Host Semaphore Set Usage Exceeds the Threshold
========================================================

Alarm Description
-----------------

The system checks the host semaphore set usage every 30 seconds. This alarm is generated when the semaphore set usage exceeds the threshold.

Host semaphore set usage = Used semaphore set/Maximum semaphore set supported by the system. By default, this alarm is reported when the host semaphore set usage is greater than 80% for three consecutive times. You can choose **O&M** > **Alarm** > **Thresholds** > **Host** > **Host Status** > **Host Semaphore Set Usage** to change the threshold.

This alarm is cleared when the host semaphore set usage is less than or equal to the threshold.

.. note::

   This alarm applies only to MRS 3.6.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12210    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+----------------------------------------------------------+
| Type                   | Parameter         | Description                                              |
+========================+===================+==========================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
| Additional Information | Trigger condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

If the host semaphore set usage exceeds the threshold, resource leakage or improper use of IPC may occur in the system. This affects the use of main OMS processes and may lead to slowed task execution, unexpected service restarts, and false reporting of other alarms.

Possible Causes
---------------

The application on the node does not release the semaphore correctly after completing operations.

Handling Procedure
------------------

**Check whether the node application is abnormal**.

#. .. _alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li4291378163548:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the alarm list, expand the alarm details, record the host name in **Location**, click the reported host name, and obtain the service IP address of the host.

#. Choose **Chart** > **Host Status**, and check whether the value of host semaphore set usage is greater than 80% (preset value).

   -  If yes, go to :ref:`3 <alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li11744358453>`.
   -  If no, go to :ref:`5 <alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li62339472163548>`.

3. .. _alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li11744358453:

   Log in to the node for which the alarm is generated using the IP address obtained in :ref:`1 <alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li4291378163548>` as user **root** and run the following command to check whether the process that uses the semaphore is returned:

   **ipcs -s -p**

   -  If yes, record the PID of the process that uses the semaphore and go to :ref:`4 <alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li71658481817>`.
   -  If no, go to :ref:`5 <alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li62339472163548>`.

4. .. _alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li71658481817:

   Run the following command to view the process details:

   **ps aux \| grep** *<pid>*

   Check whether the process logs contain error information.

   -  If yes, restart the process and go to :ref:`5 <alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li62339472163548>`.

      -  For example, if the abnormal process is httpd, run the **su-omm** command to switch to the **omm** user and run the following command to restart the process:

         **sh ${BIGDATA_HOME}/om-server/Apache-httpd-*/setup/restarthttpd.sh**

      -  For example, if the abnormal process is Manager web, run the **su-omm** command to switch to the **omm** user and run the following command to restart the process:

         **sh ${BIGDATA_HOME}/om-server/tomcat/bin/shutdown.sh;sh ${BIGDATA_HOME}/om-server/tomcat/bin/startup.sh**

   -  If no, go to :ref:`6 <alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li24184344163548>`.

5. .. _alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li62339472163548:

   Check whether the alarm is cleared 5 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li24184344163548>`.

**Collect fault information.**

6. .. _alm-12210__en-us_topic_0000002520079829_en-us_topic_0000002202523938_li24184344163548:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7. Expand the **Service** drop-down list, and select **OMS** for the target cluster. Select the host name recorded in the alarm location information.

8. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
