:original_name: mrs_01_1863.html

.. _mrs_01_1863:

Adding a Ranger Access Permission Policy for Storm
==================================================

Scenario
--------

The Ranger administrator can use Ranger to set permissions for Storm users.

Prerequisites
-------------

-  The Ranger service has been installed and is running properly.
-  You have created users, user groups, or roles for which you want to configure permissions.
-  The Ranger authentication function has been enabled on the page. The option in the following figure controls whether to enable the Ranger plug-in for permission control. If the function is enabled, the Ranger authentication is used. Otherwise, the authentication mechanism of the component is used.

Procedure
---------

#. Log in to the Ranger web UI. Click **Storm** in the **STORM** area on the homepage.

#. Click **Add New Policy** to add a Storm permission control policy.

#. Configure the parameters listed in the table below based on the service demands.

   .. table:: **Table 1** Storm permission parameters

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                               |
      +===================================+===========================================================================================================================================================================================================================================================================================================+
      | Policy Conditions                 | IP address filtering policy, which can be customized. You can enter one or more IP addresses or IP address segments. The IP address can contain the wildcard character (``*``), for example, **192.168.1.10**,\ **192.168.1.20**, or **192.168.1.\***.                                                    |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Policy Name                       | Policy name, which can be customized and must be unique in the service.                                                                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                                                                                                                                           |
      |                                   | The **include** policy applies to the current input object, and the **exclude** policy applies to objects other than the current input object.                                                                                                                                                            |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Policy Label                      | A label specified for the current policy. You can search for reports and filter policies based on labels.                                                                                                                                                                                                 |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Storm Topology                    | Name of the topology to which the current policy applies. One or more values can be entered.                                                                                                                                                                                                              |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                       | Policy description.                                                                                                                                                                                                                                                                                       |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Audit Logging                     | Whether to audit the policy.                                                                                                                                                                                                                                                                              |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Allow Conditions                  | Policy allowed condition. You can configure permissions and exceptions allowed by the policy.                                                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                           |
      |                                   | In the **Select Role**, **Select Group**, and **Select User** columns, select the role, user group, or user to which the permission is to be granted, click **Add Conditions**, add the IP address range to which the policy applies, and click **Add Permissions** to add the corresponding permissions. |
      |                                   |                                                                                                                                                                                                                                                                                                           |
      |                                   | -  **Submit Topology**: Submit a topology.                                                                                                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                                                                                                           |
      |                                   |    .. note::                                                                                                                                                                                                                                                                                              |
      |                                   |                                                                                                                                                                                                                                                                                                           |
      |                                   |       The Submit Topology permission takes effect only when **Storm Topology** is set to **\***.                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                                                           |
      |                                   | -  **File Upload**: Upload a file.                                                                                                                                                                                                                                                                        |
      |                                   | -  **File Download**: Download a file.                                                                                                                                                                                                                                                                    |
      |                                   | -  **Kill Topology**: Delete a topology.                                                                                                                                                                                                                                                                  |
      |                                   | -  **Rebalance**: Perform the rebalance operation.                                                                                                                                                                                                                                                        |
      |                                   | -  **Activate**: Activate the topology permission.                                                                                                                                                                                                                                                        |
      |                                   | -  **Deactivate**: Deactivate the topology permission.                                                                                                                                                                                                                                                    |
      |                                   | -  **Get Topology Conf**: Obtain topology configurations.                                                                                                                                                                                                                                                 |
      |                                   | -  **Get Topology**: Obtain a topology.                                                                                                                                                                                                                                                                   |
      |                                   | -  **Get User Topology**: Obtain user's topology.                                                                                                                                                                                                                                                         |
      |                                   | -  **Get Topology Info**: Obtain topology information.                                                                                                                                                                                                                                                    |
      |                                   | -  **Upload New Credential**: Upload a new credential.                                                                                                                                                                                                                                                    |
      |                                   | -  **Select/Deselect All**: Select or deselect all.                                                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                           |
      |                                   | To add multiple permission control rules, click |image1|.                                                                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                           |
      |                                   | If users or user groups in the current condition need to manage this policy, select **Delegate Admin**. These users will become the agent administrators. The agent administrators can update and delete this policy and create sub-policies based on the original policy.                                |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Deny Conditions                   | Policy rejection condition, which is used to configure the permissions and exceptions to be denied in the policy. The configuration method is similar to that of **Allow Conditions**.                                                                                                                    |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. (Optional) Add the validity period of the policy. Click **Add Validity period** in the upper right corner of the page, set **Start Time** and **End Time**, and select **Time Zone**. Click **Save**. To add multiple policy validity periods, click |image2|. To delete a policy validity period, click |image3|.

#. Click **Add** to view the basic information about the policy in the policy list. After the policy takes effect, check whether the related permissions are normal.

   To disable a policy, click |image4| to edit the policy and set the policy to **Disabled**.

   If a policy is no longer used, click |image5| to delete it.

.. |image1| image:: /_static/images/en-us_image_0000001348770097.png
.. |image2| image:: /_static/images/en-us_image_0000001349289377.png
.. |image3| image:: /_static/images/en-us_image_0000001349169805.png
.. |image4| image:: /_static/images/en-us_image_0000001295770280.png
.. |image5| image:: /_static/images/en-us_image_0000001349169809.png
