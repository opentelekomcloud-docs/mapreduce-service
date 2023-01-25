:original_name: mrs_01_24259.html

.. _mrs_01_24259:

Changing the Subnet of a Cluster
================================

If the current subnet does not have sufficient IP addresses, you can change to another subnet in the same VPC of the current cluster to obtain more available subnet IP addresses. Changing a subnet does not affect the IP addresses or subnets of existing nodes.

For details about how to configure network ACL outbound rules, see :ref:`How Do I Configure a Network ACL Outbound Rule? <mrs_01_24259__section1070017367443>`

Changing a Subnet When No Network ACL Is Associated
---------------------------------------------------

#. Log in to the MRS console.

#. Click the target cluster name to go to its details page.

#. Click **Change Subnet** on the right of **Default Subnet**.

#. Select the target subnet and click **OK**.

   If no subnet is available, click **Create Subnet** to create a subnet first.

Changing a Subnet When a Network ACL Is Associated
--------------------------------------------------

#. Log in to the MRS console and click the target cluster to go to its details page.

#. .. _mrs_01_24259__li169975160296:

   In the **Basic Information** area, view **VPC**.

#. .. _mrs_01_24259__li16830135519358:

   Log in to the VPC console. In the navigation pane on the left, choose **Virtual Private Cloud** and obtain the IPv4 CIDR block corresponding to the VPC obtained in :ref:`2 <mrs_01_24259__li169975160296>`.

#. .. _mrs_01_24259__li69549305519:

   Choose **Access Control** > **Network ACLs** and click the name of the network ACL that is associated with the default and new subnets.

   .. note::

      If both the default and new subnets are associated with a network ACL, add inbound rules to the network ACL by referring to :ref:`5 <mrs_01_24259__li1734493314818>` to :ref:`7 <mrs_01_24259__li13751204692115>`.


   .. figure:: /_static/images/en-us_image_0000001348738033.png
      :alt: **Figure 1** Network ACLs

      **Figure 1** Network ACLs

#. .. _mrs_01_24259__li1734493314818:

   On the **Inbound Rules** page, choose **More** > **Insert Rule Above** in the **Operation** column.

#. Add a network ACL rule. Set **Action** to **Allow**, **Source** to the VPC IPv4 CIDR block obtained in :ref:`3 <mrs_01_24259__li16830135519358>`, and retain the default values for other parameters.

#. .. _mrs_01_24259__li13751204692115:

   Click **OK**.

   .. note::

      If you do not want to allow access from all IPv4 CIDR blocks of the VPC, add the IPv4 CIDR blocks of the default and new subnets by performing :ref:`8 <mrs_01_24259__li211072116246>` to :ref:`12 <mrs_01_24259__li7329647202914>`. If the rules for VPC IPv4 CIDR blocks have been added, skip :ref:`8 <mrs_01_24259__li211072116246>` to :ref:`12 <mrs_01_24259__li7329647202914>`.

#. .. _mrs_01_24259__li211072116246:

   Log in to the MRS console.

#. Click the target cluster to go to its details page.

#. Click **Change Subnet** on the right of **Default Subnet**.

#. Obtain the IPv4 CIDR blocks of the default and new subnets.

   .. important::

      In this case, you do not need to click **OK** displayed in the **Change Subnet** dialog box. Otherwise, the default subnet will be updated to the new subnet, thereby making it difficult to query the IPv4 CIDR block of the default subnet. Exercise caution when performing this operation.

#. .. _mrs_01_24259__li7329647202914:

   Add the IPv4 CIDR blocks of the default and target subnets to the inbound rules of the network ACL bound to the two subnets by referring to :ref:`4 <mrs_01_24259__li69549305519>` to :ref:`7 <mrs_01_24259__li13751204692115>`.

#. Log in to the MRS console.

#. Click the target cluster to go to its details page.

#. Click **Change Subnet** on the right of **Default Subnet**.

#. Select the target subnet and click **OK**.

.. _mrs_01_24259__section1070017367443:

How Do I Configure a Network ACL Outbound Rule?
-----------------------------------------------

-  Method 1

   Allow all outbound traffic. This method ensures that clusters can be created and used properly.

-  Method 2

   Allow the mandatory outbound rules that can ensure the successful creation of clusters. You are not advised to use this method because created clusters may not run properly due to absent outbound rules. If the preceding problem occurs, contact O&M personnel.

   Similar to the example provided in method 1, set **Action** to **Allow** and add the outbound rules whose destinations are the address with **Secure Communications** enabled, NTP server address, OBS server address, OpenStack address, and DNS server address, respectively.
