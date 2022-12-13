:original_name: mrs_01_1859.html

.. _mrs_01_1859:

Adding a Ranger Access Permission Policy for Yarn
=================================================

Scenario
--------

The Ranger administrator can use Ranger to configure Yarn administrator permissions for Yarn users, allowing them to manage Yarn queue resources.

Prerequisites
-------------

-  The Ranger service has been installed and is running properly.
-  You have created users, user groups, or roles for which you want to configure permissions.

Procedure
---------

#. Log in to the Ranger management page.

#. On the home page, click the component plug-in name in the **YARN** area, for example, **Yarn**.

#. Click **Add New Policy** to add a Yarn permission control policy.

#. Configure the parameters listed in the table below based on the service demands.

   .. table:: **Table 1** Yarn permission parameters

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                              |
      +===================================+==========================================================================================================================================================================================================================================================================================================+
      | Policy Name                       | Policy name, which can be customized and must be unique in the service.                                                                                                                                                                                                                                  |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Policy Conditions                 | IP address filtering policy, which can be customized. You can enter one or more IP addresses or IP address segments. The IP address can contain the wildcard character (``*``), for example, **192.168.1.10**,\ **192.168.1.20**, or **192.168.1.\***.                                                   |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Policy Label                      | A label specified for the current policy. You can search for reports and filter policies based on labels.                                                                                                                                                                                                |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Queue                             | Queue name. The wildcard (``*``) is supported.                                                                                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                          |
      |                                   | To enable a sub-queue to inherit the permission of its upper-level queue, enable the recursion function.                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                          |
      |                                   | -  **Non-recursive**: recursion disabled                                                                                                                                                                                                                                                                 |
      |                                   | -  **Recursive**: recursion enabled                                                                                                                                                                                                                                                                      |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                       | Policy description.                                                                                                                                                                                                                                                                                      |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Audit Logging                     | Whether to audit the policy.                                                                                                                                                                                                                                                                             |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Allow Conditions                  | Policy allowed condition. You can configure permissions and exceptions allowed by the policy.                                                                                                                                                                                                            |
      |                                   |                                                                                                                                                                                                                                                                                                          |
      |                                   | In the **Select Role**, **Select Group**, and **Select User** columns, select the role, user group, or user to which the permission is to be granted, click **Add Conditions**, add the IP address range to which the policy applies, and click **Add Permissions** to add the corresponding permission. |
      |                                   |                                                                                                                                                                                                                                                                                                          |
      |                                   | -  submit-app: permission to submit queue tasks                                                                                                                                                                                                                                                          |
      |                                   | -  admin-queue: permission to manage queue tasks                                                                                                                                                                                                                                                         |
      |                                   | -  Select/Deselect All: Select or deselect all.                                                                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                                                          |
      |                                   | If users or user groups in the current condition need to manage this policy, select **Delegate Admin**. These users will become the agent administrators. The agent administrators can update and delete this policy and create sub-policies based on the original policy.                               |
      |                                   |                                                                                                                                                                                                                                                                                                          |
      |                                   | To add multiple permission control rules, click |image1|. To delete a permission control rule, click |image2|.                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                                                                          |
      |                                   | Exclude from Allow Conditions: policy exception conditions                                                                                                                                                                                                                                               |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Deny All Other Accesses           | Whether to reject all other access requests.                                                                                                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                          |
      |                                   | -  True: All other access requests are rejected.                                                                                                                                                                                                                                                         |
      |                                   | -  **False**: **Deny Conditions** can be configured.                                                                                                                                                                                                                                                     |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Deny Conditions                   | Policy rejection condition, which is used to configure the permissions and exceptions to be denied in the policy. The configuration method is similar to that of **Allow Conditions**. The priority of **Deny Conditions** is higher than that of allowed conditions configured in **Allow Conditions**. |
      |                                   |                                                                                                                                                                                                                                                                                                          |
      |                                   | Exclude from Deny Conditions: exception rules excluded from the denied conditions                                                                                                                                                                                                                        |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. table:: **Table 2** Setting permissions

      +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+
      | Task                                                                        | Role Authorization                                                                                   |
      +=============================================================================+======================================================================================================+
      | Setting the Yarn administrator permission                                   | a. On the home page, click the component plug-in name in the **YARN** area, for example, **Yarn**.   |
      |                                                                             | b. Select the policy whose **Policy Name** is **all - queue** and click |image3| to edit the policy. |
      |                                                                             | c. In the **Allow Conditions** area, select a user from the **Select User** drop-down list.          |
      +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+
      | Setting the permission for a user to submit tasks in a specified Yarn queue | a. In **Queue**, specify a queue name.                                                               |
      |                                                                             | b. In the **Allow Conditions** area, select a user from the **Select User** drop-down list.          |
      |                                                                             | c. Click **Add Permissions** and select **submit-app**.                                              |
      +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+
      | Setting the permission for a user to manage tasks in a specified Yarn queue | a. In **Queue**, specify a queue name.                                                               |
      |                                                                             | b. In the **Allow Conditions** area, select a user from the **Select User** drop-down list.          |
      |                                                                             | c. Click **Add Permissions** and select **admin-queue**.                                             |
      +-----------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+

#. (Optional) Add the validity period of the policy. Click **Add Validity period** in the upper right corner of the page, set **Start Time** and **End Time**, and select **Time Zone**. Click **Save**. To add multiple policy validity periods, click |image4|. To delete a policy validity period, click |image5|.

#. Click **Add** to view the basic information about the policy in the policy list. After the policy takes effect, check whether the related permissions are normal.

   To disable a policy, click |image6| to edit the policy and set the policy to **Disabled**.

   If a policy is no longer used, click |image7| to delete it.

.. note::

   The permissions on Ranger Yarn are independent of each other. There is inclusion relationship among the permissions. Currently, the following permissions are supported:

   -  **submit-app**: permission to submit queue tasks
   -  **admin-queue**: permission to manage queue tasks

   Although the **admin-queue** has the permission to submit tasks, it does not have the inclusion relationship with the **submit-app** permission.

.. |image1| image:: /_static/images/en-us_image_0000001296249680.png
.. |image2| image:: /_static/images/en-us_image_0000001295930212.png
.. |image3| image:: /_static/images/en-us_image_0000001296249684.png
.. |image4| image:: /_static/images/en-us_image_0000001349089885.png
.. |image5| image:: /_static/images/en-us_image_0000001295770248.png
.. |image6| image:: /_static/images/en-us_image_0000001348770069.png
.. |image7| image:: /_static/images/en-us_image_0000001295770252.png
