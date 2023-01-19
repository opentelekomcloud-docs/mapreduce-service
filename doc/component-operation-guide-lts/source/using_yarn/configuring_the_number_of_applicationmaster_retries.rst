:original_name: mrs_01_0860.html

.. _mrs_01_0860:

Configuring the Number of ApplicationMaster Retries
===================================================

Scenario
--------

When resources are insufficient or ApplicationMaster fails to start, a client probably encounters running errors.

Configuration Description
-------------------------

Go to the **All Configurations** page of Yarn and enter a parameter name list in :ref:`Table 1 <mrs_01_0860__en-us_topic_0000001173949296_t5417077b8b3e4b46b7fbdef818ccc95a>` in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

.. _mrs_01_0860__en-us_topic_0000001173949296_t5417077b8b3e4b46b7fbdef818ccc95a:

.. table:: **Table 1** Parameter description

   +--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Default Value |
   +======================================+========================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+===============+
   | yarn.resourcemanager.am.max-attempts | Number of retries of the ApplicationMaster. Increasing the number of retries can prevent ApplicationMaster startup failures caused by insufficient resources. This applies to global settings of all ApplicationMasters. Each ApplicationMaster can use an API to set an independent maximum number of retries. However, the number of retries cannot be greater than the global maximum number of retries. If the value is greater than the global maximum number of retries, the ResourceManager overwrites the value to allow at least one retry. The value must be greater than or equal to **1**. | 2             |
   +--------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
