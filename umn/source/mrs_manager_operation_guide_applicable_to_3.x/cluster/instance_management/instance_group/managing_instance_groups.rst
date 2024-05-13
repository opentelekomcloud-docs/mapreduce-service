:original_name: admin_guide_000046.html

.. _admin_guide_000046:

Managing Instance Groups
========================

Scenario
--------

Instance groups can be managed on MRS Manager. That is, you can group multiple instances in the same role based on a specified principle, such as the nodes with the same hardware configuration. The modification on the configuration parameters of an instance group applies to all instances in the group.

In a large cluster, instance groups are used to improve the capability of managing instances in batches in the heterogeneous environment. After instances are grouped, the instances can be configured repeatedly to reduce redundant instance configuration items and improve system performance.

Creating an Instance Group
--------------------------

#. Log in to MRS Manager.

#. Choose **Cluster** > *Name of the desired cluster* > **Services**.

#. Click the specified service name on the service management page.

#. On the displayed page, click the **Instance Groups** tab.

   Click |image1| and configure parameters as prompted.

   .. table:: **Table 1** Instance group configuration parameters

      +--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter          | Description                                                                                                                                                                                                                                                         |
      +====================+=====================================================================================================================================================================================================================================================================+
      | **The group name** | Indicates the instance group name. The value can contain only letters, digits, underscores (_), hyphens (-), and spaces. It must start with a letter, digit, underscore (_), or hyphen (-) and cannot ends with a space. It can contain a maximum of 99 characters. |
      +--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | **Role**           | Indicates the role to which an instance group belongs.                                                                                                                                                                                                              |
      +--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | **Copy From**      | Indicates that the parameter values of a specified instance group are copied to the parameters of a new group. If the value is null, the default values are used for the parameters of the new group.                                                               |
      +--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | **Description**    | Indicates the instance group description. It can contain only letters, digits, commas (,), periods (.), underscores (_), spaces, and line breaks, and can contain a maximum of 200 characters.                                                                      |
      +--------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      -  Each instance must belong to only one instance group. When an instance is installed for the first time, it belongs to the instance group *Role name*\ ``-``\ **DEFAULT** by default.
      -  You can delete unnecessary or unused instance groups. Before deleting an instance group, migrate all instances in the group to other instance groups, and then delete the instance group by referring to :ref:`Deleting an Instance Group <admin_guide_000046__section10369132812451>`. The default instance group cannot be deleted.

#. Click **OK**.

   The instance group is created.

Modifying Properties of an Instance Group
-----------------------------------------

#. Log in to MRS Manager.

#. Choose **Cluster** > *Name of the desired cluster* > **Services**.

#. Click the specified service name on the service management page.

#. Click the **Instance Groups** tab. On the **Instance Groups** tab page, locate the row that contains the target instance group.

   Click |image2| and modify parameters as prompted.

#. Click **OK** to save the modifications.

   The default instance group cannot be modified.

.. _admin_guide_000046__section10369132812451:

Deleting an Instance Group
--------------------------

#. Log in to MRS Manager.

#. Choose **Cluster** > *Name of the desired cluster* > **Services**.

#. Click the specified service name on the service management page.

#. Click the **Instance Groups** tab. On the **Instance Groups** tab page, locate the row that contains the target instance group.

#. Click |image3|.

#. In the displayed dialog box, click **OK**.

   The default instance group cannot be deleted.

.. |image1| image:: /_static/images/en-us_image_0000001442413917.png
.. |image2| image:: /_static/images/en-us_image_0000001392414446.png
.. |image3| image:: /_static/images/en-us_image_0000001442773673.png
