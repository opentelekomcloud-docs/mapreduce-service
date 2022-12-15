:original_name: mrs_01_2080.html

.. _mrs_01_2080:

Why Are Local Logs Not Deleted After YARN Is Restarted?
=======================================================

Question
--------

If Yarn is restarted in either of the following scenarios, local logs will not be deleted as scheduled and will be retained permanently:

-  When Yarn is restarted during task running, local logs are not deleted.
-  When the task is complete and logs fail to be collected, restart Yarn before the logs are cleared as scheduled. In this case, local logs are not deleted.

Answer
------

NodeManager has a restart recovery mechanism (for details, see https://hadoop.apache.org/docs/r3.1.1/hadoop-yarn/hadoop-yarn-site/NodeManager.html#NodeManager_Restart). Go to the **All Configurations** page of Yarn by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`. Set **yarn.nodemanager.recovery.enabled** of NodeManager to **true** to make the configuration take effect. The default value is **true**. In this way, redundant local logs are periodically deleted when the YARN is restarted.
