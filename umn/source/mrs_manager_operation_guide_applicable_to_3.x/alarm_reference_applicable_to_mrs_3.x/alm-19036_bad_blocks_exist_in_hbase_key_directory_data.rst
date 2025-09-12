:original_name: ALM-19036.html

.. _ALM-19036:

ALM-19036 Bad Blocks Exist in HBase Key Directory Data
======================================================

Alarm Description
-----------------

The system checks for bad blocks in HBase key directories every 5 minutes, including the **hbase.version** file and the **hbase:meta** and **master:store** table directories. This alarm is generated when a bad block is detected.

This alarm is cleared when the system detects that no bad blocks exist in the HBase key directories.

This alarm applies only to MRS 3.5.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
19036    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

+----------------------+-------------+----------------------------------------------------------+
| Type                 | Parameter   | Description                                              |
+======================+=============+==========================================================+
| Location Information | Source      | Specifies the cluster for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

If block loss occurs in HBase key directories, the HBase service becomes unavailable, causing service request stacking or interruptions.

Possible Causes
---------------

HDFS is faulty.

Handling Procedure
------------------

.. important::

   Handling bad blocks in key directory data involves operations that quickly restore the HBase service, such as stopping the HBase service. Be mindful that these operations will interrupt services. Also, be aware of any data stacking on the services.

**Check whether the HDFS service is normal.**

#. Log in to MRS Manager, choose **Cluster** > **Services** > **HDFS**, and check whether the HDFS running status is **Normal**.

   -  If yes, go to :ref:`3 <alm-19036__en-us_topic_0000001961820588_li22451194396>`.
   -  If no, go to :ref:`2 <alm-19036__en-us_topic_0000001961820588_li142523198391>`.

#. .. _alm-19036__en-us_topic_0000001961820588_li142523198391:

   Restore the HDFS running status to **Normal** by following the instructions provided in the alarm help, and go to :ref:`3 <alm-19036__en-us_topic_0000001961820588_li22451194396>`.

**Rebuild key directory data.**

3. .. _alm-19036__en-us_topic_0000001961820588_li22451194396:

   Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, check the cause of the alarm whose **Alarm ID** is **19036**, and identify the directory with block loss.

4. Perform the restoration operations based on the directory where block loss has occurred.

   -  If **Alarm Cause** indicates that bad blocks exist in the **hbase.version** file, go to :ref:`5 <alm-19036__en-us_topic_0000001961820588_li667865418432>` to restore the **hbase.version** file.
   -  If **Alarm Cause** indicates that bad blocks exist in the **hbase:meta** table directory, go to :ref:`6 <alm-19036__en-us_topic_0000001961820588_li7729173404414>` to restore the **hbase meta** table directory files.
   -  If **Alarm Cause** indicates that bad blocks exist in the **master:store** table directory, go to :ref:`7 <alm-19036__en-us_topic_0000001961820588_li204135201921>` to restore the **master store** table directory files.

5. .. _alm-19036__en-us_topic_0000001961820588_li667865418432:

   Restore the **hbase.version** file.

   a. Log in to the node where the client is installed as the client installation user.

   b. Run the following command to go to the client installation directory:

      **cd** *Client installation directory*

   c. Run the following commands to configure environment variables:

      **source bigdata_env**

      **source HBase/component_env**

   d. Kerberos authentication is enabled for the cluster (the cluster is in security mode): Run the following command to authenticate as the HBase built-in user. If this is your first-time authentication, enter the default password and change it.

      **kinit** **hbase**

      Kerberos authentication is disabled for the cluster (the cluster is in normal mode): Run the following command to set the Hadoop username:

      **export HADOOP_USER_NAME=hbase**

   e. Run the following command to create a backup directory that does not exist in HDFS, for example, **/tmp/hbase_bak**:

      **hdfs dfs -mkdir** */tmp/hbase_bak*

   f. Run the following command to back up the old file:

      **hdfs dfs -mv /hbase/hbase.version** */tmp/hbase_bak*

   g. Run the following command to restore the **hbase.version** file:

      **hbase hbck -j** **${HBASE_HOME}/tools/hbase-hbck2-*.jar filesystem -fixVersionFile**

      -  After the command is executed successfully, run the following command to view the restored **hbase.version** file:

         **hdfs dfs -ls /hbase**

      -  If the command fails to be executed, go to :ref:`8 <alm-19036__en-us_topic_0000001961820588_li08848474240>`.

   h. Log in to MRS Manager, choose **Cluster** > **Services** > **HBase** > **Instances**, select all HMaster instances, click **More**, and select **Instance Rolling Restart**. In the dialog box that is displayed, enter the password of the current user, and click **OK** to perform a rolling restart of all HMaster instances.

   i. After the HMaster instances are restarted, check whether the alarm is cleared in the alarm list.

      -  If yes, no further action is required.
      -  If no, go to :ref:`8 <alm-19036__en-us_topic_0000001961820588_li08848474240>`.

6. .. _alm-19036__en-us_topic_0000001961820588_li7729173404414:

   Restore the **hbase meta** table directory files.

   a. Log in to MRS Manager, choose **Cluster** > **Services** > **HBase**, and click **Stop Service** in the upper right corner of the **Dashboard** page. In the dialog box that is displayed, enter the password of the current user and click **OK** to stop the HBase service.

   b. Log in to the node where the client is installed as the client installation user.

   c. Run the following command to go to the client installation directory:

      **cd** *Client installation directory*

   d. Run the following commands to configure environment variables:

      **source bigdata_env**

      **source HBase/component_env**

   e. Kerberos authentication is enabled for the cluster (the cluster is in security mode): Run the following command to authenticate as the HBase built-in user. If this is your first-time authentication, enter the default password and change it.

      **kinit** **hbase**

      Kerberos authentication is disabled for the cluster (the cluster is in normal mode): Run the following command to set the Hadoop username:

      **export HADOOP_USER_NAME=hbase**

   f. Run the following commands to regenerate the **meta** table data:

      **export HBASE_CLASSPATH=${HBASE_CLASSPATH}:${HBASE_HOME}/tools/\***

      **hbase org.apache.hbase.hbck1.OfflineMetaRepair -details**

      If **Success** is displayed, the command is successfully executed. In this case, go to :ref:`6.g <alm-19036__en-us_topic_0000001961820588_li12724121120>`. If the command fails to be executed, go to :ref:`8 <alm-19036__en-us_topic_0000001961820588_li08848474240>`.

   g. .. _alm-19036__en-us_topic_0000001961820588_li12724121120:

      Run the following command to create a backup directory that does not exist in HDFS, for example, **/tmp/hbase_bak**:

      **hdfs dfs -mkdir** */tmp/hbase_bak*

   h. Run the following command to back up and clear HMaster data:

      **hdfs dfs -mv /hbase/MasterData/\*** */tmp/hbase_bak*

   i. Run the following commands to clear the location information of the **meta** table:

      **hbase zkcli**

      **deleteall /hbase/meta-region-server**

      **quit**

   j. Log in to MRS Manager, choose **Cluster** > **Services** > **HBase**, and click **Start Service** in the upper right corner of the **Dashboard** page to start the HBase service.

   k. After the HBase service is started, check whether the alarm is cleared in the alarm list.

      -  If yes, no further action is required.
      -  If no, go to :ref:`8 <alm-19036__en-us_topic_0000001961820588_li08848474240>`.

7. .. _alm-19036__en-us_topic_0000001961820588_li204135201921:

   Restore the **master store** table directory files.

   a. Log in to MRS Manager, choose **Cluster** > **Services** > **HBase**, and click **Stop Service** in the upper right corner of the **Dashboard** page. In the dialog box that is displayed, enter the password of the current user and click **OK** to stop the HBase service.

   b. Log in to the node where the client is installed as the client installation user.

   c. Run the following command to go to the client installation directory:

      **cd** *Client installation directory*

   d. Run the following commands to configure environment variables:

      **source bigdata_env**

      **source HBase/component_env**

   e. Kerberos authentication is enabled for the cluster (the cluster is in security mode): Run the following command to authenticate as the HBase built-in user. If this is your first-time authentication, enter the default password and change it.

      **kinit** **hbase**

      Kerberos authentication is disabled for the cluster (the cluster is in normal mode): Run the following command to set the Hadoop username:

      **export HADOOP_USER_NAME=hbase**

   f. Run the following command to create a backup directory that does not exist in HDFS, for example, **/tmp/hbase_bak**:

      **hdfs dfs -mkdir** */tmp/hbase_bak*

   g. Run the following command to back up and clear HMaster data:

      **hdfs dfs -mv /hbase/MasterData/\*** */tmp/hbase_bak*

   h. Run the following commands to clear the location information of the **meta** table:

      **hbase zkcli**

      **deleteall /hbase/meta-region-server**

      **quit**

   i. Log in to MRS Manager, choose **Cluster** > **Services** > **HBase**, and click **Start Service** in the upper right corner of the **Dashboard** page to start the HBase service.

   j. After the HBase service is started, check whether the alarm is cleared in the alarm list.

      -  If yes, no further action is required.
      -  If no, go to :ref:`8 <alm-19036__en-us_topic_0000001961820588_li08848474240>`.

.. note::

   After the HBase service is restored, observe the service for a period of time. After confirming that HBase and related services are normal, you are advised to run the following command to delete the backup directory to prevent residual useless files:

   **hdfs dfs -rm -r** */tmp/hbase_bak*

**Collect fault information.**

8.  .. _alm-19036__en-us_topic_0000001961820588_li08848474240:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **HBase** for the target cluster.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
