:original_name: ALM-14036.html

.. _ALM-14036:

ALM-14036 NameNode Is In Safe Mode
==================================

This alarm applies only to MRS 3.3.1 or later.

Alarm Description
-----------------

The system checks the NameNode process status every 30 seconds. This alarm is generated when the NameNode is in the safe mode.

This alarm is cleared when the process status recovers.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
14036    Major          Yes
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
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

After a NameNode enters the safe mode, data cannot be written to the NameNode.

Possible Causes
---------------

Block loss occurs when a user manually enters the safe mode or restarts the NameNode.

Handling Procedure
------------------

**Check whether NameNode is in the security mode.**

#. .. _alm-14036__li099993153914:

   Log in to MRS Manager, click **O&M**, and choose **Alarm** > **Alarms** to view the alarm details. In the **Location** column, check the name of the host for which the alarm is generated.

#. Choose **Cluster** > **Services** > **HDFS**, and click **NameNode(**\ *host name recorded in :ref:`1 <alm-14036__li099993153914>`,x*\ **)** next to **NameNode Web UI**.

   .. note::

      By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

#. In the **Basic Information** area on the **Dashboard** page of HDFS (or in the **NameService Summary** area on the **Dashboard** page of HDFS), check whether the value of **Safe Mode** is **ON**.

   **ON** indicates that the safe mode is enabled.

   -  If yes, go to :ref:`4 <alm-14036__li19115623192816>`.
   -  If no, go to :ref:`7 <alm-14036__li17799174711116>`.

#. .. _alm-14036__li19115623192816:

   Log in to the HDFS client.

   a. Log in to the node where the HDFS client is installed.

      -  If Kerberos authentication is enabled for the cluster (the cluster is in security mode), log in as the **root** user.
      -  If Kerberos authentication is disabled for the cluster (the cluster is in normal mode), log in as user **omm** and ensure that user **omm** has the execute permission on the client.

      (Note that you need to decide with cluster security/normal mode, not the HDFS safe/common mode.)

   b. Run the following commands to go to the client installation directory and configure environment variables:

      **cd** *HDFS client installation directory*

      **source bigdata_env**

   c. If Kerberos authentication is enabled for the cluster (the cluster is in security mode), run the following command to authenticate the user. If Kerberos authentication is disabled for the cluster (the cluster is in normal mode), skip this step.

      **kinit hdfs**

      Enter the password as prompted. You can obtain the password from the MRS cluster administrator. Change the password upon the first authentication.

   d. Run the following command to exit from the safe mode:

      **hdfs dfsadmin -safemode leave**

#. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, go to :ref:`6 <alm-14036__li18278458174317>`.
   -  If no, go to :ref:`7 <alm-14036__li17799174711116>`.

#. .. _alm-14036__li18278458174317:

   In the **Basic Information** area on the **Dashboard** page of HDFS (or in the **NameService Summary** area on the **Dashboard** page of HDFS), check whether the value of **Missing Blocks** is **0**.

   -  If yes, no further action is required.
   -  If no, check whether "ALM-14003 Number of Lost HDFS Blocks Exceeds the Threshold" is reported and rectify the fault according to the alarm help.

**Collect fault information.**

7.  .. _alm-14036__li17799174711116:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **HDFS** for the target cluster.

9.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
