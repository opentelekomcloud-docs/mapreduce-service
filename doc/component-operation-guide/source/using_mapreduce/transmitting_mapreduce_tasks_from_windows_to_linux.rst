:original_name: mrs_01_0838.html

.. _mrs_01_0838:

Transmitting MapReduce Tasks from Windows to Linux
==================================================

Scenarios
---------

If you want to transmit a job from Windows to Linux, set **mapreduce.app-submission.cross-platform** to **true**. If this parameter is unavailable for a cluster or its value is **false**, the function of transmitting MapReduce tasks from Windows to Linux is not supported. In this case, perform the following operations to add this parameter or change its value to enable this function:

.. note::

   This section applies to MRS 3.\ *x* or later.

Configuration Description
-------------------------

Adjust the following parameter in the **mapred-site.xml** configuration file on the client to enable the running of MapReduce tasks: The **mapred-site.xml** configuration file is in the **config** directory of the client installation path, for example, **/opt/client/Yarn/config**.

.. table:: **Table 1** Parameters

   +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                               | Description                                                                                                                                                                                                                                                                          | Default Value |
   +=========================================+======================================================================================================================================================================================================================================================================================+===============+
   | mapreduce.app-submission.cross-platform | Indicates whether to support running of MapReduce tasks after they are transmitted from Windows to Linux. When the parameter value is **true**, the running of MapReduce tasks is supported. When the parameter value is **false**, the running of MapReduce tasks is not supported. | true          |
   +-----------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
