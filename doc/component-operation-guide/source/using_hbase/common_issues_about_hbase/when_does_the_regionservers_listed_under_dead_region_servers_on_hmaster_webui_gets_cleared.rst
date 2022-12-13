:original_name: mrs_01_1649.html

.. _mrs_01_1649:

When does the RegionServers listed under "Dead Region Servers" on HMaster WebUI gets cleared?
=============================================================================================

Question
--------

When does the RegionServers listed under "Dead Region Servers" on HMaster WebUI gets cleared?

Answer
------

When an online RegionServer goes down abruptly, it is displayed under "Dead Region Servers" in the HMaster WebUI. When dead RegionServer restarts and reports back to HMaster successfully, the "Dead Region Servers" in the HMaster WebUI gets cleared.

The "Dead Region Servers" is also gets cleared, when the HMaster failover operation is performed successfully.

In cases when an Active HMaster hosting some regions is abruptly killed, Backup HMaster will become the new Active HMater and displays previous Active HMaster as dead RegionServer.
