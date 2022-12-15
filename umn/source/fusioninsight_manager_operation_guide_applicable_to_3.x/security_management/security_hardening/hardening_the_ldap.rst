:original_name: admin_guide_000280.html

.. _admin_guide_000280:

Hardening the LDAP
==================

Configuring the LDAP Firewall Policy
------------------------------------

In the cluster adopting the dual-plane networking, the LDAP is deployed on the service plane. To ensure the LDAP data security, you are advised to configure the firewall policy in the cluster to disable relevant LDAP ports.

#. Log in to FusionInsight Manager.
#. Click **Cluster**, click the name of the desired cluster, choose **Services** > **LdapServer**, and click **Configurations**.
#. Check the value of **LDAP_SERVER_PORT**, which is the service port of LdapServer.
#. To ensure data security, configure the firewall policy for the whole cluster to disable the LdapServer port based on the customer's firewall environment.

Enabling the LDAP Audit Log Output
----------------------------------

Users can set the audit log output level of the LDAP service and output audit logs in a specified directory, for example, **/var/log/messages**. The logs output can be used to check user activities and operation commands.

.. note::

   If the function of LDAP audit log output is enabled, massive logs are generated, affecting the cluster performance. Exercise caution when enabling this function.

#. Log in to any LdapServer node.

#. Run the following command to edit the **slapd.conf.consumer** file, and set the value of **loglevel** to **256** (you can run the **man slapd.conf** command on the OS to view the log level definition).

   **cd ${BIGDATA_HOME}/FusionInsight_BASE\_8.1.0.1/install/FusionInsight-ldapserver-2.7.0/ldapserver/local/template**

   **vi slapd.conf.consumer**

   .. code-block::

      ...
      pidfile         [PID_FILE_SLAPD_PID]
      argsfile        [PID_FILE_SLAPD_ARGS]
      loglevel   256
      ...

#. Log in to FusionInsight Manager, click **Cluster**, click the name of the desired cluster, choose **Services** > **LdapServer**. On the displayed page, choose **More** > **Restart Service**. Enter the administrator password and restart the service.
