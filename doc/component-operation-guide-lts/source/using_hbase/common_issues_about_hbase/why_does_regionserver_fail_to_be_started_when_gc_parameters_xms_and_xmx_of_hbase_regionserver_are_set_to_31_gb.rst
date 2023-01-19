:original_name: mrs_01_1661.html

.. _mrs_01_1661:

Why Does RegionServer Fail to Be Started When GC Parameters Xms and Xmx of HBase RegionServer Are Set to 31 GB?
===============================================================================================================

Question
--------

Check the **hbase-omm-*.out** log of the node where RegionServer fails to be started. It is found that the log contains **An error report file with more information is saved as: /tmp/hs_err_pid*.log**. Check the **/tmp/hs_err_pid*.log** file. It is found that the log contains **#Internal Error (vtableStubs_aarch64.cpp:213), pid=9456, tid=0x0000ffff97fdd200 and #guarantee(_\_ pc() <= s->code_end()) failed: overflowed buffer**, indicating that the problem is caused by JDK. How do I solve this problem?

Answer
------

To rectify the fault, perform the following steps:

#. Run the **su - omm** command on a node where RegionServer fails to be started to switch to user **omm**.

#. Run the **java -XX:+PrintFlagsFinal -version \|grep HeapBase** command as user **omm**. Information similar to the following is displayed:

   .. code-block::

      uintx HeapBaseMinAddress = 2147483648 {pd product}

#. Change the values of **-Xms** and **-Xmx** in **GC_OPTS** to values that are not between **32G-HeapBaseMinAddress** and **32G**, excluding the values of **32G** and **32G-HeapBaseMinAddress**.

#. Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **Instance**, select the failed instance, and choose **More** > **Restart Instance** to restart the failed instance.
