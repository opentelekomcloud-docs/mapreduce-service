:original_name: mrs_03_1035.html

.. _mrs_03_1035:

How Do I Assign Tenant Management Permission to a New Account?
==============================================================

You can assign tenant management permission only in analysis or hybrid clusters, but not in streaming clusters.

The operations vary depending on the MRS cluster version:

**Procedure for versions earlier than MRS cluster 3.x:**

#. Log in to MRS Manager as user **admin**.
#. Choose **System** > **Manage User**. Select the new account, and click **Modify** in the **Operation** column.
#. In **Assign Rights by Role**, click **Select and Add Role**.

   -  If you bind the **Manager_tenant** role to the account, the account will have permission to view tenant management information.
   -  If you bind the **Manager_administrator** role to the account, the account will have permission to view and perform tenant management.

#. Click **OK**.

**Procedure for MRS cluster 3.x and later versions:**

#. Log in to MRS Manager and choose **System** > **Permission** > **User**.

#. Locate the user and click **Modify**.

   Modify the parameters based on service requirements.

   If you bind the **Manager_tenant** role to the account, the account will have permission to view tenant management information. If you bind the **Manager_administrator** role to the account, the account will have permission to perform tenant management and view related information.

   .. note::

      It takes about three minutes for the settings to take effect after user group or role permission are modified.

#. Click **OK**.
