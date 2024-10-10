:original_name: mrs_01_248987.html

.. _mrs_01_248987:

Scenarios
=========

Configuring Storage and Compute Decoupling
------------------------------------------

#. Create an MRS cluster.

   The MRS cluster must contain basic components such as Guardian, Ranger, and Hadoop.

   .. note::

      Currently, only MRS 3.3.0-LTS and later versions support interconnection with OBS using the Guardian component.

#. Create an OBS agency.

   Create an agency with OBS access permissions, which is used for interconnecting Guardian with OBS.

#. Enable the interconnection between Guardian and OBS and configure parameters.

   Modify the configuration parameters for the Guardian service and configure the IAM agency authentication information.

#. Configure the policy for clearing component data in the recycle bin directory.

   In the storage-compute decoupling scenario, the prevention against accidental deletion is enabled by default for components connected to OBS. When a user deletes data, the deleted object is moved to the corresponding recycle bin directory. You need to configure a lifecycle rule for the corresponding directory in the OBS file system to prevent the storage space from being used up.

#. Interconnect components with OBS.

   Components in the MRS cluster can directly access the corresponding path after the required permissions for accessing OBS buckets are obtained. You can use the component client to directly access resources in the OBS file system in absolute path mode.

Configuring OBS Permissions
---------------------------

If Guardian is deployed with decoupled storage and compute and Ranger authentication is enabled for MRS clusters, Ranger administrators can configure read and write permissions on OBS directories or files for cluster users.

With the Guardian permission model, storage and compute decoupling, and Hive cascading authorization, authorization is not required after the first permission service table authorization on the Ranger page and the system automatically associates the permissions of OBS data storage source in a fine-grained manner. The storage path of the table does not need to be sensed.

.. note::

   -  On the Ranger page, OBS permission authorization only support Manager custom user groups (built-in user groups are not supported). The user group contains a maximum of 52 characters, including digits 0 to 9, letters A to Z, underscores (_), and number signs (#). Otherwise, the policy fails to be added.
   -  For clusters with Kerberos authentication enabled, permissions need to be granted based on Ranger. For clusters with Kerberos authentication disabled, OBS permissions are granted by default, and no additional configuration is required.
   -  If Kerberos authentication is not enabled for the current cluster, the user who accesses OBS must belong to the **supergroup** group.
