:original_name: ALM-12062.html

.. _ALM-12062:

ALM-12062 OMS Parameter Configurations Mismatch with the Cluster Scale
======================================================================

Description
-----------

The system checks whether the OMS parameter configurations match with the cluster scale at each top hour. If the OMS parameter configurations do not meet the cluster scale requirements, the system generates this alarm. This alarm is automatically cleared when the OMS parameter configurations are modified.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12062    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+---------------------------------------------------------------------+
| Parameter   | Description                                                         |
+=============+=====================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated.   |
+-------------+---------------------------------------------------------------------+
| ServiceName | Specifies the name of the service for which the alarm is generated. |
+-------------+---------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.                |
+-------------+---------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.                |
+-------------+---------------------------------------------------------------------+

Impact on the System
--------------------

The OMS configuration is not modified when the cluster is installed or the system capacity is expanded.

Possible Causes
---------------

The OMS parameter configurations mismatch with the cluster scale.

Procedure
---------

**Check whether the OMS parameter configurations match with the cluster scale.**

#. In the alarm list on MRS Manager, locate the row that contains the alarm, and view the IP address of the host for which the alarm is generated.
#. Log in to the host where the alarm is generated as user **root**.
#. Run the **su - omm** command to switch to user **omm**.
#. Run the **vi $BIGDATA_LOG_HOME/controller/scriptlog/modify_manager_param.log** command to open the log file and search for the log file containing the following information: Current oms configurations cannot support *xx* nodes. In the information, *xx* indicates the number of nodes in the cluster.
#. Optimize the current cluster configuration by following the instructions in :ref:`Optimizing Manager Configurations Based on the Number of Cluster Nodes <alm-12062__section117861721171717>`.
#. One hour later, check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`7 <alm-12062__li8140111212587>`.

**Collect fault information.**

7.  .. _alm-12062__li8140111212587:

    On MRS Manager, choose **O&M** > **Log** > **Download**.

8.  Select **Controller** from the **Service** and click **OK**.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

.. _alm-12062__section117861721171717:

Related Information
-------------------

**Optimizing Manager Configurations Based on the Number of Cluster Nodes**

#. Log in to the active Manager node as user **omm**.

#. Run the following command to switch the directory:

   **cd ${BIGDATA_HOME}/om-server/om/sbin**

#. Run the following command to view the current Manager configurations.

   **sh oms_config_info.sh -q**

#. Run the following command to specify the number of nodes in the current cluster.

   Command format: **sh oms_config_info.sh -s** *number of nodes*

   Example:

   **sh oms_config_info.sh -s 1000**

   Enter **y** as prompted.

   .. code-block::

      The following configurations will be modified:
           Module       Parameter         Current          Target
           Controller   controller.Xmx    4096m        =>  16384m
           Controller   controller.Xms    1024m        =>  8192m
           Controller   controller.node.heartbeat.error.threshold     30000                      =>   60000
           Pms          pms.mem           8192m        =>  10240m
      Do you really want to do this operation? (y/n):

   The configurations are updated successfully if the following information is displayed:

   .. code-block::

      ...
      Operation has been completed. Now restarting OMS server.                  [done]
      Restarted oms server successfully.

   .. note::

      -  OMS is automatically restarted during the configuration update process.
      -  Clusters with similar quantities of nodes have same Manager configurations. For example, when the number of nodes is changed from 100 to 101, no configuration item needs to be updated.

.. |image1| image:: /_static/images/en-us_image_0000001532607874.png
