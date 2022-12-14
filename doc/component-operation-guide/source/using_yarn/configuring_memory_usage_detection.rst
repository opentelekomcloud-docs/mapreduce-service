:original_name: mrs_01_0863.html

.. _mrs_01_0863:

Configuring Memory Usage Detection
==================================

Scenario
--------

If memory usage of the submitted application cannot be estimated, you can modify the configuration on the server to determine whether to check the memory usage.

If the memory usage is not checked, the container occupies the memory until the memory overflows. If the memory usage exceeds the configured memory size, the corresponding container is killed.

Configuration Description
-------------------------

Go to the **All Configurations** page of Yarn and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

.. table:: **Table 1** Parameter description

   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | Parameter                           | Description                                                                                                                                      | Default Value                            |
   +=====================================+==================================================================================================================================================+==========================================+
   | yarn.nodemanager.vmem-check-enabled | Whether to enable virtual memory usage detection. If the memory used by a task exceeds the allocated memory size, the task is forcibly stopped.  | For versions earlier than MRS 3.x: false |
   |                                     |                                                                                                                                                  |                                          |
   |                                     | -  If the value is **true**, the virtual memory will be checked.                                                                                 | For MRS 3.x or later: true               |
   |                                     | -  If the value is **false**, the virtual memory will not be checked.                                                                            |                                          |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
   | yarn.nodemanager.pmem-check-enabled | Whether to enable physical memory usage detection. If the memory used by a task exceeds the allocated memory size, the task is forcibly stopped. | true                                     |
   |                                     |                                                                                                                                                  |                                          |
   |                                     | -  If the value is **true**, the physical memory will be checked.                                                                                |                                          |
   |                                     | -  If the value is **false**, the physical memory will not be checked.                                                                           |                                          |
   +-------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------------------+
