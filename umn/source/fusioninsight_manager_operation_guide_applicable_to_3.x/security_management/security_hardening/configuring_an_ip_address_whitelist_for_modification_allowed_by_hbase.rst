:original_name: admin_guide_000278.html

.. _admin_guide_000278:

Configuring an IP Address Whitelist for Modification Allowed by HBase
=====================================================================

If the Replication function is enabled for HBase clusters, a protection mechanism for data modification is added on the standby HBase cluster to ensure data consistency between the active and standby clusters. Upon receiving an RPC request for data modification, the standby HBase cluster checks the permission of the user who sends the request (only HBase manage users have the modification permission). Then it checks the validity of the source IP address of the request. Only modification requests from IP addresses in the white list are accepted. The IP address white list is configured by the **hbase.replication.allowedIPs** item.

Log in to FusionInsight Manager and choose **Cluster** > **Services** > **HBase**. Click **Configurations** and enter the parameter name in the search box.

.. table:: **Table 1** Parameter description

   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                    | Description                                                                                                                                                                                                                        | Default Value         |
   +==============================+====================================================================================================================================================================================================================================+=======================+
   | hbase.replication.allowedIPs | Allows replication request processing from configured IP addresses only. It supports comma separated regex patterns. Each pattern can be any of the following:                                                                     | N/A                   |
   |                              |                                                                                                                                                                                                                                    |                       |
   |                              | -  Regex pattern                                                                                                                                                                                                                   |                       |
   |                              |                                                                                                                                                                                                                                    |                       |
   |                              |    Example: 10.18.40.*, 10.18.*, 10.18.40.11                                                                                                                                                                                       |                       |
   |                              |                                                                                                                                                                                                                                    |                       |
   |                              | -  Range pattern (Range can be specified only in the last octet)                                                                                                                                                                   |                       |
   |                              |                                                                                                                                                                                                                                    |                       |
   |                              |    Example: 10.18.40.[10-20]                                                                                                                                                                                                       |                       |
   |                              |                                                                                                                                                                                                                                    |                       |
   |                              | If this item is empty (default value), the white list contains only the IP address of the RegionServer of the cluster, indicating that only modification requests from the RegionServer of the standby HBase cluster are accepted. |                       |
   +------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
