:original_name: admin_guide_000274.html

.. _admin_guide_000274:

Configuring a Trusted IP Address to Access LDAP
===============================================

Scenario
--------

By default, the LDAP service deployed in the OMS and cluster can be accessed by any IP address. To enable the LDAP service to be accessed by only trusted IP addresses, you can configure the INPUT policy in the iptables filtering list.

Impact on the System
--------------------

After the configuration, the LDAP service cannot be accessed by IP addresses that are not configured. Before the expansion, the added IP addresses need to be configured as trusted IP addresses.

Prerequisites
-------------

-  You have collected the management plane IP addresses and service plane IP addresses of all nodes in the cluster and all floating IP addresses.
-  You have obtained the **root** user account for all nodes in the cluster.

Procedure
---------

**Configuring trusted IP addresses for the LDAP service on the OMS**

#. Confirm the management node IP address. For details, see :ref:`Logging In to the Management Node <admin_guide_000005>`.

#. Log in to MRS Manager. For details, see :ref:`Logging In to MRS Manager <admin_guide_000004>`.

#. Choose **System** > **OMS** and choose **oldap** > **Modify Configuration** to view the OMS LDAP port number, that is, the value of **LDAP Listening Port**. The default port number is **21750**.

#. Log in to the active management node as user **root** using the IP address of the active management node.

#. .. _admin_guide_000274__li727167195016:

   Run the following command to check the INPUT policy in the iptables filtering list:

   **iptables -L**

   For example, if no rule is configured, the INPUT policy is displayed as follows:

   .. code-block::

      Chain INPUT (policy ACCEPT)
      target     prot opt source               destination

#. Run the following command to configure all IP addresses used by the cluster as trusted IP addresses. Each IP address needs to be added independently.

   **iptables -A INPUT -s** *Trusted IP address* **-p tcp --dport** *Port number* **-j ACCEPT**

   For example, to configure **10.0.0.1** as a trusted IP address and enable it to access port **21750**, you need to run the following command:

   **iptables -A INPUT -s 10.0.0.1 -p tcp --dport 21750 -j ACCEPT**

#. Run the following command to configure all IP addresses as untrusted IP addresses. The trusted IP addresses will not be affected by this rule.

   **iptables -A INPUT -p tcp --dport** *Port number* **-j DROP**

   For example, to disable all IP addresses to access port **21750**, run the following command:

   **iptables -A INPUT -p tcp --dport 21750 -j DROP**

#. Run the following command to view the modified INPUT policy in the iptables filtering list:

   **iptables -L**

   For example, after a trusted IP address is configured, the INPUT policy is displayed as follows:

   .. code-block::

      Chain INPUT (policy ACCEPT)
      target     prot opt source               destination
      ACCEPT     tcp  --  10.0.0.1             anywhere            tcp dpt:21750
      DROP       tcp  --  anywhere             anywhere            tcp dpt:21750

#. Run the following command to view the rules and rule numbers in the iptables filtering list:

   **iptables -L -n --line-number**

   .. code-block::

      Chain INPUT (policy ACCEPT)
      num target     prot opt source               destination
      1   DROP       tcp  --  0.0.0.0/0            0.0.0.0/0           tcp dpt:21750

#. .. _admin_guide_000274__li28581039195016:

   Run the following command to delete the desired rule from the iptables filtering list based on site requirement:

   **iptables -D INPUT** *Number of the rule to be deleted*

   For example, to delete rule 1, run the following command:

   **iptables -D INPUT 1**

#. Log in to the standby management node as user **root** using the standby IP address. Repeat :ref:`5 <admin_guide_000274__li727167195016>` to :ref:`10 <admin_guide_000274__li28581039195016>`.

**Configuring trusted IP addresses for the LDAP service in the cluster**

12. Log in to MRS Manager.

13. Click **Cluster**, click the name of the desired cluster, and choose **Service** > **LdapServer**. On the displayed page, click **Instance** to view the nodes where the LDAP services locate.

14. Go to the **Configurations** page, and view the LDAP port number of the cluster, that is, the value of **LDAP_SERVER_PORT**. The default value is **21780**.

15. Log in to the LDAP node as user **root** using the LDAP service IP address.

16. .. _admin_guide_000274__li41253757195016:

    Run the following command to view the INPUT policy in the iptables filtering list:

    **iptables -L**

    For example, if no rule is configured, the INPUT policy is displayed as follows:

    .. code-block::

       Chain INPUT (policy ACCEPT)
       target     prot opt source               destination

17. Run the following command to configure all IP addresses used by the cluster as trusted IP addresses. Each IP address needs to be added independently.

    **iptables -A INPUT -s** *Trusted IP address* **-p tcp --dport** *Port number* **-j ACCEPT**

    For example, to configure **10.0.0.1** as a trusted IP address and enable it to access port **21780**, you need to run the following command:

    **iptables -A INPUT -s 10.0.0.1 -p tcp --dport 21780 -j ACCEPT**

18. Run the following command to configure all IP addresses as untrusted IP addresses. The trusted IP addresses will not be affected by this rule.

    **iptables -A INPUT -p tcp --dport** *Port number* **-j DROP**

    For example, to disable all IP addresses to access port **21780**, run the following command:

    **iptables -A INPUT -p tcp --dport 21780 -j DROP**

19. Run the following command to view the modified INPUT policy in the iptables filtering list:

    **iptables -L**

    For example, after a trusted IP address is configured, the INPUT policy is displayed as follows:

    .. code-block::

       Chain INPUT (policy ACCEPT)
       target     prot opt source               destination
       ACCEPT     tcp  --  10.0.0.1             anywhere            tcp dpt:21780
       DROP       tcp  --  anywhere             anywhere            tcp dpt:21780

20. Run the following command to view the rules and rule numbers in the iptables filtering list:

    **iptables -L -n --line-number**

    .. code-block::

       Chain INPUT (policy ACCEPT)
       num target     prot opt source               destination
       1   DROP       tcp  --  0.0.0.0/0            0.0.0.0/0           tcp dpt:21780

21. .. _admin_guide_000274__li48007687195016:

    Run the following command to delete the desired rule from the iptables filtering list based on site requirement:

    **iptables -D INPUT** *Number of the rule to be deleted*

    For example, to delete rule 1, run the following command:

    **iptables -D INPUT 1**

22. Log in to the LDAP node as user **root** using the IP address of another LDAP service, and repeat :ref:`16 <admin_guide_000274__li41253757195016>` to :ref:`21 <admin_guide_000274__li48007687195016>`.
