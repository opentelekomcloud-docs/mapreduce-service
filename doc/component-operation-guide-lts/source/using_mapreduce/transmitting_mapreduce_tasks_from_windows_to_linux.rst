:original_name: mrs_01_0838.html

.. _mrs_01_0838:

Transmitting MapReduce Tasks from Windows to Linux
==================================================

Scenarios
---------

To submit MapReduce tasks from Windows to Linux, set **mapreduce.app-submission.cross-platform** to **true**. If this parameter does not exist in the cluster or the value of this parameter is **false**, the cluster does not support this function. Perform the following operations to add this parameter or change the value of this parameter to enable it.

Configuration Description
-------------------------

Adjust the following parameter in the **mapred-site.xml** configuration file on the client to enable the running of MapReduce tasks: The **mapred-site.xml** configuration file is in the **conf** directory of the client installation path, for example, **/opt/client/Yarn/config**.

.. table:: **Table 1** Parameters

   +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                               | Description                                                                                                                                                                                                                                                                          | Default Value |
   +=========================================+======================================================================================================================================================================================================================================================================================+===============+
   | mapreduce.app-submission.cross-platform | Indicates whether to support running of MapReduce tasks after they are transmitted from Windows to Linux. When the parameter value is **true**, the running of MapReduce tasks is supported. When the parameter value is **false**, the running of MapReduce tasks is not supported. | true          |
   +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
