:original_name: mrs_01_0536.html

.. _mrs_01_0536:

Configuring a Static Service Pool
=================================

Scenario
--------

If you need to control the node resources that can be used by the cluster service or the CPU usage of the node used by the cluster in different time periods, you can adjust the resource base on MRS Manager and customize the resource configuration groups.

Prerequisites
-------------

-  After the static service pool is configured, the HDFS and YARN services need to be restarted. During the restart, the services are unavailable.
-  After a static service pool is configured, the maximum number of resources used by each service and role instance cannot exceed the upper limit.

Procedure
---------

#. Modify the system resource adjustment base.

   a. On MRS Manager, click **System**. In the **Resource** area, click **Configure Static Service Pool**.

   b. Click **Configuration**. The service pool configuration group management page is displayed.

   c. In the **System Resource Adjustment Base** area, change the values of **CPU(%)** and **Memory(%)** .

      Modifying **System Resource Adjustment Base** limits the maximum physical CPU and memory resource percentage of nodes that can be used by the Flume, HBase, HDFS, Impala and YARN services. If multiple services are deployed on the same node, the maximum physical resource usage of all services cannot exceed the adjusted CPU or memory usage.

   d. Click **Next**.

      If you need to modify the parameters again, click **Previous** in the lower part of the page.

#. Modify the **default** configuration group of the service pool.

   a. Click **default**. In the **Service Pool Configuration** table, set **CPU LIMIT(%)**, **CPU SHARE(%)**, **I/O(%)**, and **Memory(%)** for the Flume, HBase, HDFS, Impala and YARN services.

   .. note::

      -  The sum of **CPU LIMIT(%)** used by all services can exceed 100%.
      -  The sum of **CPU SHARE(%)** and **I/O(%)** used by all services must be 100%. For example, if CPU resources are allocated to the HDFS and Yarn services, the total CPU resources allocated to the two services are 100%.
      -  The sum of **Memory(%)** used by all services can be greater than, smaller than, or equal to 100%.
      -  **Memory(%)** cannot take effect dynamically and can only be modified in the default configuration group.

   b. Click in the blank area of the page to complete the editing. MRS Manager generates the correct values of service pool parameters in the **Detailed Configuration** area based on the cluster hardware resources and allocation information.

   c. You can click |image1| on the right of **Detailed Configuration** to modify the parameter values of the service pool based on service requirements.

      In the **Service Pool Configuration** area, click the specified service name. The **Detailed Configuration** area displays only the parameters of the service. Manual changing of parameter values does not refresh the service resource usage. In added configuration groups, the configuration group numbers of the parameters that take effect dynamically will be displayed. For example, **HBase: RegionServer: dynamic-config1.RES_CPUSET_PERCENTAGE**. The parameter functions do not change.

      .. table:: **Table 1** Parameters of the static service pool

         +------------------------------------------+---------------------------------------------------------------------------------+
         | Parameter                                | Description                                                                     |
         +==========================================+=================================================================================+
         | -  RES_CPUSET_PERCENTAGE                 | Configures the service CPU percentage.                                          |
         | -  dynamic-configX.RES_CPUSET_PERCENTAGE |                                                                                 |
         +------------------------------------------+---------------------------------------------------------------------------------+
         | -  RES_CPU_SHARE                         | Configures the service CPU share.                                               |
         | -  dynamic-configX.RES_CPU_SHARE         |                                                                                 |
         +------------------------------------------+---------------------------------------------------------------------------------+
         | -  RES_BLKIO_WEIGHT                      | Configures service I/O usage.                                                   |
         | -  dynamic-configX.RES_BLKIO_WEIGHT      |                                                                                 |
         +------------------------------------------+---------------------------------------------------------------------------------+
         | HBASE_HEAPSIZE                           | Configures the maximum JVM memory for RegionServer.                             |
         +------------------------------------------+---------------------------------------------------------------------------------+
         | HADOOP_HEAPSIZE                          | Configures the maximum JVM memory of a DataNode.                                |
         +------------------------------------------+---------------------------------------------------------------------------------+
         | yarn.nodemanager.resource.memory-mb      | Configures the memory that can be used by NodeManager on the current node.      |
         +------------------------------------------+---------------------------------------------------------------------------------+
         | dfs.datanode.max.locked.memory           | Configures the maximum memory that can be used by a DataNode as the HDFS cache. |
         +------------------------------------------+---------------------------------------------------------------------------------+
         | FLUME_HEAPSIZE                           | Configures the maximum JVM memory that can be used by each Flume instance.      |
         +------------------------------------------+---------------------------------------------------------------------------------+
         | IMPALAD_MEM_LIMIT                        | Configures the maximum memory that can be used by an Impalad instance.          |
         +------------------------------------------+---------------------------------------------------------------------------------+

#. Add a customized resource configuration group.

   a. Determine whether to automatically adjust resource configurations based on the time.

      If yes, go to :ref:`3.b <mrs_01_0536__en-us_topic_0035209694_li207277341970>`.

      If no, go to :ref:`4 <mrs_01_0536__en-us_topic_0035209694_li5675506119820>`.

   b. .. _mrs_01_0536__en-us_topic_0035209694_li207277341970:

      Click |image2| to add a resource configuration group. In the **Scheduling Time** area, click |image3|. The time policy configuration page is displayed.

      Modify the following parameters based on service requirements and click **OK**.

      -  **Repeat**: If selected, the resource configuration group runs repeatedly based on the scheduling period. If not selected, set the date and time when the configuration of the group of resources can be applied.
      -  **Repeat Policy**: can be set to **Daily**, **Weekly**, and **Monthly**. This parameter is valid only when **Repeat** is selected.
      -  **Between**: indicates the time period between the start time and end time when the resource configuration is applied. Set a unique time range. If the time range overlaps with that of an existing group of resource configuration, the time range cannot be saved. This parameter is valid only when **Repeat** is selected.

      .. note::

         -  The **default** group of resource configuration takes effect in all undefined time segments.
         -  The newly added resource group is a parameter set that takes effect dynamically in a specified time range.
         -  The newly added resource group can be deleted. A maximum of four resource configuration groups that take effect dynamically can be added.
         -  Select a repetition policy. If the end time is earlier than the start time, the next day is labeled by default. For example, if a validity period ranges from 22:00 to 06:00, the customized resource configuration takes effect from 22:00 on the current day to 06:00 on the next day.
         -  If the repeat policy types of multiple configuration groups are different, the time ranges can overlap. The policy types are listed as follows by priority from low to high: daily, weekly, and monthly. The following is an example. There are two resource configuration groups using the monthly and daily policies, respectively. Their application time ranges in a day overlap as follows: [04:00 to 07:00] and [06:00 to 08:00]. In this case, the configuration of the group that uses the monthly policy prevails.
         -  If the repeat policy types of multiple resource configuration groups are the same, the time ranges of different dates can overlap. For example, if there are two weekly scheduling groups, you can set the same time range on different day for them, such as to 04:00 to 07:00, on Monday and Wednesday, respectively.

   c. On the **Service Pool Configuration** page, modify the resource configuration of each service. Click the blank area on the page to complete the editing, and go to :ref:`4 <mrs_01_0536__en-us_topic_0035209694_li5675506119820>`.

      You can click |image4| on the right of **Service Pool Configuration** to modify the parameters. Click |image5| in the **Detailed Configuration** area to manually update the parameter values generated by the system based on service requirements.

#. .. _mrs_01_0536__en-us_topic_0035209694_li5675506119820:

   Saves the settings.

   Click **Save**. In the **Save Configuration** dialog box, select **Restart the affected services or instances**. Click **OK** to save the settings and restart related services.

   **Operation succeeded** is displayed. click **Finish**. The service is started successfully.

.. |image1| image:: /_static/images/en-us_image_0000002278456009.png
.. |image2| image:: /_static/images/en-us_image_0000001295738420.jpg
.. |image3| image:: /_static/images/en-us_image_0000002278456193.png
.. |image4| image:: /_static/images/en-us_image_0000002243537010.png
.. |image5| image:: /_static/images/en-us_image_0000002278536077.png
