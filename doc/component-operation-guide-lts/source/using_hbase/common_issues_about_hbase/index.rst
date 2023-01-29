:original_name: mrs_01_1638.html

.. _mrs_01_1638:

Common Issues About HBase
=========================

-  :ref:`Why Does a Client Keep Failing to Connect to a Server for a Long Time? <mrs_01_1639>`
-  :ref:`Operation Failures Occur in Stopping BulkLoad On the Client <mrs_01_1640>`
-  :ref:`Why May a Table Creation Exception Occur When HBase Deletes or Creates the Same Table Consecutively? <mrs_01_1641>`
-  :ref:`Why Other Services Become Unstable If HBase Sets up A Large Number of Connections over the Network Port? <mrs_01_1642>`
-  :ref:`Why Does the HBase BulkLoad Task (One Table Has 26 TB Data) Consisting of 210,000 Map Tasks and 10,000 Reduce Tasks Fail? <mrs_01_1643>`
-  :ref:`How Do I Restore a Region in the RIT State for a Long Time? <mrs_01_1644>`
-  :ref:`Why Does HMaster Exits Due to Timeout When Waiting for the Namespace Table to Go Online? <mrs_01_1645>`
-  :ref:`Why Does SocketTimeoutException Occur When a Client Queries HBase? <mrs_01_1646>`
-  :ref:`Why Modified and Deleted Data Can Still Be Queried by Using the Scan Command? <mrs_01_1647>`
-  :ref:`Why "java.lang.UnsatisfiedLinkError: Permission denied" exception thrown while starting HBase shell? <mrs_01_1648>`
-  :ref:`When does the RegionServers listed under "Dead Region Servers" on HMaster WebUI gets cleared? <mrs_01_1649>`
-  :ref:`Why Are Different Query Results Returned After I Use Same Query Criteria to Query Data Successfully Imported by HBase bulkload? <mrs_01_1650>`
-  :ref:`What Should I Do If I Fail to Create Tables Due to the FAILED_OPEN State of Regions? <mrs_01_1651>`
-  :ref:`How Do I Delete Residual Table Names in the /hbase/table-lock Directory of ZooKeeper? <mrs_01_1652>`
-  :ref:`Why Does HBase Become Faulty When I Set a Quota for the Directory Used by HBase in HDFS? <mrs_01_1653>`
-  :ref:`Why HMaster Times Out While Waiting for Namespace Table to be Assigned After Rebuilding Meta Using OfflineMetaRepair Tool and Startups Failed <mrs_01_1654>`
-  :ref:`Why Messages Containing FileNotFoundException and no lease Are Frequently Displayed in the HMaster Logs During the WAL Splitting Process? <mrs_01_1655>`
-  :ref:`Insufficient Rights When a Tenant Accesses Phoenix <mrs_01_1657>`
-  :ref:`What Can I Do When HBase Fails to Recover a Task and a Message Is Displayed Stating "Rollback recovery failed"? <mrs_01_1659>`
-  :ref:`How Do I Fix Region Overlapping? <mrs_01_1660>`
-  :ref:`Why Does RegionServer Fail to Be Started When GC Parameters Xms and Xmx of HBase RegionServer Are Set to 31 GB? <mrs_01_1661>`
-  :ref:`Why Does the LoadIncrementalHFiles Tool Fail to Be Executed and "Permission denied" Is Displayed When Nodes in a Cluster Are Used to Import Data in Batches? <mrs_01_0625>`
-  :ref:`Why Is the Error Message "import argparse" Displayed When the Phoenix sqlline Script Is Used? <mrs_01_2210>`
-  :ref:`How Do I Deal with the Restrictions of the Phoenix BulkLoad Tool? <mrs_01_2211>`
-  :ref:`Why a Message Is Displayed Indicating that the Permission is Insufficient When CTBase Connects to the Ranger Plug-ins? <mrs_01_2212>`

.. toctree::
   :maxdepth: 1
   :hidden: 

   why_does_a_client_keep_failing_to_connect_to_a_server_for_a_long_time
   operation_failures_occur_in_stopping_bulkload_on_the_client
   why_may_a_table_creation_exception_occur_when_hbase_deletes_or_creates_the_same_table_consecutively
   why_other_services_become_unstable_if_hbase_sets_up_a_large_number_of_connections_over_the_network_port
   why_does_the_hbase_bulkload_task_one_table_has_26_tb_data_consisting_of_210000_map_tasks_and_10000_reduce_tasks_fail
   how_do_i_restore_a_region_in_the_rit_state_for_a_long_time
   why_does_hmaster_exits_due_to_timeout_when_waiting_for_the_namespace_table_to_go_online
   why_does_sockettimeoutexception_occur_when_a_client_queries_hbase
   why_modified_and_deleted_data_can_still_be_queried_by_using_the_scan_command
   why_java.lang.unsatisfiedlinkerror_permission_denied_exception_thrown_while_starting_hbase_shell
   when_does_the_regionservers_listed_under_dead_region_servers_on_hmaster_webui_gets_cleared
   why_are_different_query_results_returned_after_i_use_same_query_criteria_to_query_data_successfully_imported_by_hbase_bulkload
   what_should_i_do_if_i_fail_to_create_tables_due_to_the_failed_open_state_of_regions
   how_do_i_delete_residual_table_names_in_the_hbase_table-lock_directory_of_zookeeper
   why_does_hbase_become_faulty_when_i_set_a_quota_for_the_directory_used_by_hbase_in_hdfs
   why_hmaster_times_out_while_waiting_for_namespace_table_to_be_assigned_after_rebuilding_meta_using_offlinemetarepair_tool_and_startups_failed
   why_messages_containing_filenotfoundexception_and_no_lease_are_frequently_displayed_in_the_hmaster_logs_during_the_wal_splitting_process
   insufficient_rights_when_a_tenant_accesses_phoenix
   what_can_i_do_when_hbase_fails_to_recover_a_task_and_a_message_is_displayed_stating_rollback_recovery_failed
   how_do_i_fix_region_overlapping
   why_does_regionserver_fail_to_be_started_when_gc_parameters_xms_and_xmx_of_hbase_regionserver_are_set_to_31_gb
   why_does_the_loadincrementalhfiles_tool_fail_to_be_executed_and_permission_denied_is_displayed_when_nodes_in_a_cluster_are_used_to_import_data_in_batches
   why_is_the_error_message_import_argparse_displayed_when_the_phoenix_sqlline_script_is_used
   how_do_i_deal_with_the_restrictions_of_the_phoenix_bulkload_tool
   why_a_message_is_displayed_indicating_that_the_permission_is_insufficient_when_ctbase_connects_to_the_ranger_plug-ins
