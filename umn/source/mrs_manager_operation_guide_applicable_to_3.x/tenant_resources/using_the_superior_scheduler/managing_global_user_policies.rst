:original_name: admin_guide_000115.html

.. _admin_guide_000115:

Managing Global User Policies
=============================

Scenario
--------

If a tenant uses a Superior scheduler, you can configure the global policy for users to use the resource scheduler, including:

-  Maximum running apps
-  Maximum pending apps
-  Default queue

Procedure
---------

-  Add a policy.

   #. On MRS Manager, choose **Tenant Resources**.
   #. Choose **Dynamic Resource Plan**.
   #. Click the **Global User Policy** tab.

      .. note::

         **defaults(default setting)** indicates that the policy specified for **defaults** is used if a user does not have a global policy. The default policy cannot be deleted.

   #. Click **Create Global User Policy**. In the displayed dialog box, set the following parameters:

      -  **Cluster**: Select the target cluster.
      -  **Username**: indicates the user for whom resource scheduling is controlled. Enter an existing username in the current cluster.
      -  **Max Running Apps**: indicates the maximum number of tasks that the user can run in the current cluster.
      -  **Max Pending Apps**: indicates the maximum number of tasks that the user can suspend in the current cluster.
      -  **Default Queue**: indicates the queue of the user. Enter the name of an existing queue in the current cluster.

-  Modify a policy.

   #. On MRS Manager, choose **Tenant Resources**.
   #. Choose **Dynamic Resource Plan**.
   #. Click the **Global User Policy** tab.
   #. In the row that contains the desired user policy, click **Modify** in the **Operation** column.
   #. In the displayed dialog box, modify parameters and click **OK**.

-  Delete a policy.

   #. On MRS Manager, choose **Tenant Resources**.

   #. Choose **Dynamic Resource Plan**.

   #. Click the **Global User Policy** tab.

   #. In the row that contains the desired user policy, click **Delete** in the **Operation** column.

      In the displayed dialog box, click **OK**.
