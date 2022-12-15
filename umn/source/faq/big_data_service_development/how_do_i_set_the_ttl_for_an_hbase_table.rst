:original_name: mrs_03_1140.html

.. _mrs_03_1140:

How Do I Set the TTL for an HBase Table?
========================================

-  Set the time to live (TTL) when creating a table:

   Create the **t_task_log** table, set the column family to **f**, and set the TTL to **86400** seconds.

   .. code-block::

      create 't_task_log',{NAME => 'f', TTL=>'86400'}

-  Set the TTL for an existing table:

   .. code-block::

      disable "t_task_log" #Disable the table (services must be stopped).
      alter "t_task_log",NAME=>'data',TTL=>'86400' # Set the TTL value for the column family data.
      enable "t_task_log" #Restore the table.
