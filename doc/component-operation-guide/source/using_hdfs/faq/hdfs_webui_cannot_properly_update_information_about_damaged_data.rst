:original_name: mrs_01_1694.html

.. _mrs_01_1694:

HDFS WebUI Cannot Properly Update Information About Damaged Data
================================================================

Question
--------

#. When errors occur in the **dfs.datanode.data.dir** directory of DataNode due to the permission or disk damage, HDFS WebUI does not display information about damaged data.
#. After errors are restored, HDFS WebUI does not timely remove related information about damaged data.

Answer
------

#. DataNode checks whether the disk is normal only when errors occur in file operations. Therefore, only when a data damage is detected and the error is reported to NameNode, NameNode displays information about the damaged data on HDFS WebUI.
#. After errors are fixed, you need to restart DataNode. During restarting DataNode, all data states are checked and damaged data information is uploaded to NameNode. Therefore, after errors are fixed, damaged data information is not displayed on the HDFS WebUI only by restarting DataNode.
