:original_name: admin_guide_000196.html

.. _admin_guide_000196:

Configuring the Number of Local Audit Log Backups
=================================================

Scenario
--------

Audit logs of cluster components are classified by name and stored in the **/var/log/Bigdata/audit** directory on each cluster node. The OMS automatically backs up the audit log directories at 03:00 every day.

The audit log directory on each node is compressed and named in the *<Node IP address>*\ **.tar.gz** format. All compressed files are compressed and named in the *<yyyy-MM-dd_HH-mm-ss>*\ **.tar.gz** format and saved in the **/var/log/Bigdata/audit/bk/** directory on the active management node. In addition, the standby management node saves a copy of the file.

By default, a maximum of 90 OMS backup files can be retained. This section describes how to configure the maximum number.

Procedure
---------

#. Log in to the active management node as user **omm**.

   .. note::

      Perform this operation only on the active management node. This operation is not supported on the standby management nodes; otherwise, the cluster cannot work properly.

#. Run the following command to switch to the required directory:

   **cd ${BIGDATA_HOME}/om-server/om/sbin**

#. Run the following command to change the maximum number of audit log backup files to be retained:

   **./modifyLogConfig.sh -m** **Maximum number of backup files that can be retained**

   The default value is **90**. The value ranges from **0** to **365**. A larger value means to consume more disk space.

   If the following information is displayed, the operation is successful:

   .. code-block::

      Modify log config successfully
