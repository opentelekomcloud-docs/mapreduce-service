:original_name: mrs_01_0455.html

.. _mrs_01_0455:

Creating a Custom Policy
========================

Custom policies can be created to supplement the system-defined policies of MRS. For the actions that can be added to custom policies, see **Permissions Policies and Supported Actions** > **Introduction** in MapReduce Service API Reference.

You can create custom policies in either of the following ways:

-  Visual editor: Select cloud services, actions, resources, and request conditions. This does not require knowledge of policy syntax.
-  JSON: Edit JSON policies from scratch or based on an existing policy.

Example Custom Policies
-----------------------

-  Example 1: Allowing users to create MRS clusters only

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "mrs:cluster:create",
                      "ecs:*:*",
                      "bms:*:*",
                      "evs:*:*",
                      "vpc:*:*",
                      "smn:*:*"
                  ]
              }
          ]
      }

-  Example 2: Allowing users to resize an MRS cluster

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "mrs:cluster:resize"
                  ]
              }
          ]
      }

-  Example 3: Allowing users to create a cluster, create and execute a job, and delete a single job, but denying cluster deletion

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "mrs:cluster:create",
                      "mrs:job:submit",
                      "mrs:job:delete"
                  ]
              },
              {
                  "Effect": "Deny",
                  "Action": [
                      "mrs:cluster:delete"
                  ]
              }
          ]
      }

-  Example 4: Allowing users to create an ECS cluster with the minimum permission

   .. note::

      -  If you need a key pair when creating a cluster, add the following permissions: **ecs:serverKeypairs:get** and **ecs:serverKeypairs:list**.
      -  Add the **kms:cmk:list** permission when encrypting data disks during cluster creation.
      -  Add the **mrs:alarm:subscribe** permission to enable the alarm function during cluster creation.
      -  Add the **rds:instance:list** permission to use external data sources during cluster creation.

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "mrs:cluster:create"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "ecs:cloudServers:updateMetadata",
                      "ecs:cloudServerFlavors:get",
                      "ecs:cloudServerQuotas:get",
                      "ecs:servers:list",
                      "ecs:servers:get",
                      "ecs:cloudServers:delete",
                      "ecs:cloudServers:list",
                      "ecs:serverInterfaces:get",
                      "ecs:serverGroups:manage",
                      "ecs:servers:setMetadata",
                      "ecs:cloudServers:get",
                      "ecs:cloudServers:create"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "vpc:securityGroups:create",
                      "vpc:securityGroupRules:delete",
                      "vpc:vpcs:create",
                      "vpc:ports:create",
                      "vpc:securityGroups:get",
                      "vpc:subnets:create",
                      "vpc:privateIps:delete",
                      "vpc:quotas:list",
                      "vpc:networks:get",
                      "vpc:publicIps:list",
                      "vpc:securityGroups:delete",
                      "vpc:securityGroupRules:create",
                      "vpc:privateIps:create",
                      "vpc:ports:get",
                      "vpc:ports:delete",
                      "vpc:publicIps:update",
                      "vpc:subnets:get",
                      "vpc:publicIps:get",
                      "vpc:ports:update",
                      "vpc:vpcs:list"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "evs:quotas:get",
                      "evs:types:get"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "bms:serverFlavors:get"
                  ]
              }
          ]
      }

-  Example 5: Allowing users to create a BMS cluster with the minimum permission

   .. note::

      -  If you need a key pair when creating a cluster, add the following permissions: **ecs:serverKeypairs:get** and **ecs:serverKeypairs:list**.
      -  Add the **kms:cmk:list** permission when encrypting data disks during cluster creation.
      -  Add the **mrs:alarm:subscribe** permission to enable the alarm function during cluster creation.
      -  Add the **rds:instance:list** permission to use external data sources during cluster creation.

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "mrs:cluster:create"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "ecs:servers:list",
                      "ecs:servers:get",
                      "ecs:cloudServers:delete",
                      "ecs:serverInterfaces:get",
                      "ecs:serverGroups:manage",
                      "ecs:servers:setMetadata",
                      "ecs:cloudServers:create",
                      "ecs:cloudServerFlavors:get",
                      "ecs:cloudServerQuotas:get"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "vpc:securityGroups:create",
                      "vpc:securityGroupRules:delete",
                      "vpc:vpcs:create",
                      "vpc:ports:create",
                      "vpc:securityGroups:get",
                      "vpc:subnets:create",
                      "vpc:privateIps:delete",
                      "vpc:quotas:list",
                      "vpc:networks:get",
                      "vpc:publicIps:list",
                      "vpc:securityGroups:delete",
                      "vpc:securityGroupRules:create",
                      "vpc:privateIps:create",
                      "vpc:ports:get",
                      "vpc:ports:delete",
                      "vpc:publicIps:update",
                      "vpc:subnets:get",
                      "vpc:publicIps:get",
                      "vpc:ports:update",
                      "vpc:vpcs:list"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "evs:quotas:get",
                      "evs:types:get"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "bms:servers:get",
                      "bms:servers:list",
                      "bms:serverQuotas:get",
                      "bms:servers:updateMetadata",
                      "bms:serverFlavors:get"
                  ]
              }
          ]
      }

-  Example 6: Allowing users to create a hybrid ECS and BMS cluster with the minimum permission

   .. note::

      -  If you need a key pair when creating a cluster, add the following permissions: **ecs:serverKeypairs:get** and **ecs:serverKeypairs:list**.
      -  Add the **kms:cmk:list** permission when encrypting data disks during cluster creation.
      -  Add the **mrs:alarm:subscribe** permission to enable the alarm function during cluster creation.
      -  Add the **rds:instance:list** permission to use external data sources during cluster creation.

   .. code-block::

      {
          "Version": "1.1",
          "Statement": [
              {
                  "Effect": "Allow",
                  "Action": [
                      "mrs:cluster:create"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "ecs:cloudServers:updateMetadata",
                      "ecs:cloudServerFlavors:get",
                      "ecs:cloudServerQuotas:get",
                      "ecs:servers:list",
                      "ecs:servers:get",
                      "ecs:cloudServers:delete",
                      "ecs:cloudServers:list",
                      "ecs:serverInterfaces:get",
                      "ecs:serverGroups:manage",
                      "ecs:servers:setMetadata",
                      "ecs:cloudServers:get",
                      "ecs:cloudServers:create"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "vpc:securityGroups:create",
                      "vpc:securityGroupRules:delete",
                      "vpc:vpcs:create",
                      "vpc:ports:create",
                      "vpc:securityGroups:get",
                      "vpc:subnets:create",
                      "vpc:privateIps:delete",
                      "vpc:quotas:list",
                      "vpc:networks:get",
                      "vpc:publicIps:list",
                      "vpc:securityGroups:delete",
                      "vpc:securityGroupRules:create",
                      "vpc:privateIps:create",
                      "vpc:ports:get",
                      "vpc:ports:delete",
                      "vpc:publicIps:update",
                      "vpc:subnets:get",
                      "vpc:publicIps:get",
                      "vpc:ports:update",
                      "vpc:vpcs:list"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "evs:quotas:get",
                      "evs:types:get"
                  ]
              },
              {
                  "Effect": "Allow",
                  "Action": [
                      "bms:servers:get",
                      "bms:servers:list",
                      "bms:serverQuotas:get",
                      "bms:servers:updateMetadata",
                      "bms:serverFlavors:get"
                  ]
              }
          ]
      }
