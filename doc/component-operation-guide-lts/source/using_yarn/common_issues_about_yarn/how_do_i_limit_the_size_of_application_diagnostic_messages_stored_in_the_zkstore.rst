:original_name: mrs_01_2090.html

.. _mrs_01_2090:

How Do I Limit the Size of Application Diagnostic Messages Stored in the ZKstore?
=================================================================================

Question
--------

How do I limit the size of application diagnostic messages stored in the ZKstore?

Answer
------

In some cases, it has been observed that diagnostic messages may grow infinitely. Because diagnostic messages are stored in the ZKstore, it is not recommended that you allow diagnostic messages to grow indefinitely. Therefore, a property parameter is needed to set the maximum size of the diagnostic message.

If you need to set **yarn.app.attempt.diagnostics.limit.kc**, go to the **All Configurations** page by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>` and search for the following parameters in the search box:

.. table:: **Table 1** Parameter description

   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Default Value |
   +=======================================+==========================================================================================================================================================================================================================================================================================================================================================================================================================================================================+===============+
   | yarn.app.attempt.diagnostics.limit.kc | Data size of the diagnosis message for each application connection, in kilobytes (number of characters x 1,024). When ZooKeeper is used to store the behavior status of applications, the size of diagnosis messages needs to be limited to prevent Yarn from overloading ZooKeeper. If **yarn.resourcemanager.state-store.max-completed-applications** is set to a large value, you need to decrease the value of this property to limit the total size of stored data. | 64            |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
