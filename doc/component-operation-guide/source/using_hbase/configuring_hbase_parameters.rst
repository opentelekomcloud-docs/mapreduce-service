:original_name: mrs_01_0443.html

.. _mrs_01_0443:

Configuring HBase Parameters
============================

.. note::

   The operations described in this section apply only to clusters of versions earlier than MRS 3.x.

If the default parameter settings of the MRS service cannot meet your requirements, you can modify the parameter settings as required.

#. Log in to the service page.

   For versions earlier than MRS 1.9.2: Log in to MRS Manager, and choose **Services**.

   For MRS 1.9.2 or later: Click the cluster name on the MRS console and choose **Components**.

#. Choose **HBase** > **Service Configuration** and switch **Basic** to **All**. On the displayed HBase configuration page, modify parameter settings.

   .. table:: **Table 1** HBase parameters

      +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------+
      | Parameter                             | Description                                                                                                                                                                                                                                                           | Value                           |
      +=======================================+=======================================================================================================================================================================================================================================================================+=================================+
      | hbase.regionserver.hfile.durable.sync | Whether to enable the HFile durability to make data persistence on disks. If this parameter is set to **true**, HBase performance is affected because each HFile is synchronized to disks by **hadoop fsync** when being written to HBase.                            | Possible values are as follows: |
      |                                       |                                                                                                                                                                                                                                                                       |                                 |
      |                                       | This parameter exists only in MRS 1.9.2 or earlier.                                                                                                                                                                                                                   | -  **true**                     |
      |                                       |                                                                                                                                                                                                                                                                       | -  **false**                    |
      |                                       |                                                                                                                                                                                                                                                                       |                                 |
      |                                       |                                                                                                                                                                                                                                                                       | The default value is **true**.  |
      +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------+
      | hbase.regionserver.wal.durable.sync   | Specifies whether to enable WAL file durability to make the WAL data persistence on disks. If this parameter is set to **true**, HBase performance is affected because each edited WAL file is synchronized to disks by **hadoop fsync** when being written to HBase. | Possible values are as follows: |
      |                                       |                                                                                                                                                                                                                                                                       |                                 |
      |                                       | This parameter exists only in MRS 1.9.2 or earlier.                                                                                                                                                                                                                   | -  **true**                     |
      |                                       |                                                                                                                                                                                                                                                                       | -  **false**                    |
      |                                       |                                                                                                                                                                                                                                                                       |                                 |
      |                                       |                                                                                                                                                                                                                                                                       | The default value is **true**.  |
      +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------+
