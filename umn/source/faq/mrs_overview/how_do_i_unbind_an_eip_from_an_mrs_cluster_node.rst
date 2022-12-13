:original_name: mrs_03_1246.html

.. _mrs_03_1246:

How Do I Unbind an EIP from an MRS Cluster Node?
================================================

Symptom
-------

After an EIP is bound on the console, the EIP cannot be unbound in the EIP module of the VPC service.

A dialog box is displayed, indicating that the operation cannot be performed because the EIP is being used by MapReduce.

Procedure
---------

#. Log in to the VPC console and choose **Virtual Private Cloud** > **My VPCs**. Find the target VPC in the VPC list.
#. Click the VPC name to go to the **Summary** tab page and click the number next to **Subnets** in the **Networking Components** area to find the subnet to which the cluster belongs.
#. In the subnet list, click the target subnet name. Click the **IP Addresses** tab, locate the target public IP address and click **Unbind from EIP** in the **Operation** column.
