:original_name: admin_guide_000019.html

.. _admin_guide_000019:

Configuring Cluster Static Resources
====================================

Scenario
--------

You can adjust resource base on MRS Manager and customize resource configuration groups if you need to control service resources used on each node in a cluster or the available CPU or I/O quotas on each node at different time segments.

Impact on the System
--------------------

-  After a static service pool is configured, the configuration status of affected services is displayed as **Expired**. You need to restart the services. Services are unavailable during restart.
-  After a static service pool is configured, the maximum number of resources used by each service and role instance cannot exceed the upper limit.

Procedure
---------

**Modify the Resource Adjustment Base**

#. On MRS Manager, choose **Cluster**, click the name of the target cluster, and choose **Static Service Pool Configurations**.

#. Click **Configuration** in the upper right corner. The page for configuring resource pools is displayed.

#. Change the values of **CPU (%)** and **Memory (%)** in the **System Resource Adjustment Base** area.

   Modifying the system resource adjustment base changes the maximum physical CPU and memory usage on nodes by services. If multiple services are deployed on the same node, the maximum physical resource usage of all services cannot exceed the adjusted CPU or memory usage.

#. Click **Next**.

   To modify parameters again, click **Previous**.

**Modify the Default Resource Configuration Group**

5. Click **default**. In the **Configure weight** table, set **CPU LIMIT(%)**, **CPU SHARE(%)**, **I/O(%)**, and **Memory(%)** for each service.

   .. note::

      -  The sum of **CPU LIMIT(%)** and **CPU SHARE(%)** used by all services can exceed 100%.
      -  The sum of **I/O(%)** used by all services can exceed 100% but cannot be 0.
      -  The sum of **Memory(%)** used by all services can be greater than, smaller than, or equal to 100%.
      -  **Memory(%)** cannot take effect dynamically and can only be modified in the default configuration group.
      -  **CPU LIMIT(%)** is used to configure the ratio of the number of CPU cores that can be used by a service to those can be allocated to related nodes.
      -  **CPU SHARE(%**) is used to configure the ratio of the time when a service uses a CPU core to the time when other services use the CPU core. That is, the ratio of time when multiple services compete for the same CPU core.

6. Click **Generate detailed configurations based on weight configurations**. MRS Manager generates the actual values of the parameters in the default weight configuration table based on the cluster hardware resources and allocation information.

7. Click **OK**.

   In the displayed dialog box, click **OK**.

**Add a Customized Resource Configuration Group**

8.  Determine whether to automatically adjust resource configurations at different time segments.

    -  If yes, go to :ref:`9 <admin_guide_000019__li1535819244375>`.
    -  If no, use the default configurations, and no further action is required.

9.  .. _admin_guide_000019__li1535819244375:

    Click **Configuration**, change the system resource adjustment base values, and click **Next**.

10. Click **Add** to add a resource configuration group.

11. In **Step 1: Scheduling Time**, click **Configuration**.

    The page for configuring the time policy is displayed.

    Modify the following parameters based on service requirements and click **OK**.

    -  **Repeat**: If this parameter is selected, the customized resource configuration is applied repeatedly based on the scheduling period. If this parameter is not selected, set the date and time when the configuration of the group of resources can be applied.
    -  **Repeat Policy**: The available values are **Daily**, **Weekly**, and **Monthly**. This parameter is valid only when **Repeat** is selected.
    -  **On**: indicates the time period between the start time and end time when the resource configuration is applied. Set a unique time range. If the time range overlaps with that of an existing group of resource configuration, the time range cannot be saved.

    .. note::

       -  The default group of resource configuration takes effect in all undefined time segments.
       -  The newly added resource group is a parameter set that takes effect dynamically in a specified time range.
       -  The newly added resource group can be deleted. A maximum of four resource configuration groups that take effect dynamically can be added.
       -  Select a repetition policy. If the end time is earlier than the start time, the resource configuration ends in the next day by default. For example, if a validity period ranges from 22:00 to 06:00, the customized resource configuration takes effect from 22:00 on the current day to 06:00 on the next day.
       -  If the repetition policy types of multiple configuration groups are different, the time ranges can overlap. The policy types are listed as follows by priority from low to high: daily, weekly, and monthly. The following is an example. There are two resource configuration groups using the monthly and daily policies, respectively. Their application time ranges in a day overlap as follows: 04:00 to 07:00 and 06:00 to 08:00. In this case, the configuration of the group that uses the monthly policy prevails.
       -  If the repetition policy types of multiple resource configuration groups are the same, the time ranges of different dates can overlap. For example, if there are two weekly scheduling groups, you can set the same time range on different day for them, such as to 04:00 to 07:00, on Monday and Wednesday, respectively.

12. Modify the resource configuration of each service in **Step 2: Weight Configuration**.

13. Click **Generate detailed configuration**. MRS Manager generates the actual values of the parameters in the default weight configuration table based on the cluster hardware resources and allocation information.

14. Click **OK**.

    In the displayed dialog box, click **OK**.
