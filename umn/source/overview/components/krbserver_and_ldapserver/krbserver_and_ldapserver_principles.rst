:original_name: mrs_08_00641.html

.. _mrs_08_00641:

KrbServer and LdapServer Principles
===================================

Overview
--------

To manage the access control permissions on data and resources in a cluster, it is recommended that the cluster be installed in security mode. In security mode, a client application must be authenticated and a secure session must be established before the application accesses any resource in the cluster. MRS uses KrbServer to provide Kerberos authentication for all components, implementing a reliable authentication mechanism.

LdapServer supports Lightweight Directory Access Protocol (LDAP) and provides the capability of storing user and user group data for Kerberos authentication.

Architecture
------------

The security authentication function for user login depends on Kerberos and LDAP.

.. _mrs_08_00641__fig6453372512431:

.. figure:: /_static/images/en-us_image_0000001349309949.png
   :alt: **Figure 1** Security authentication architecture

   **Figure 1** Security authentication architecture

:ref:`Figure 1 <mrs_08_00641__fig6453372512431>` includes three scenarios:

-  Logging in to the MRS Manager Web UI

   The authentication architecture includes steps 1, 2, 3, and 4.

-  Logging in to a component web UI

   The authentication architecture includes steps 5, 6, 7, and 8.

-  Accessing between components

   The authentication architecture includes step 9.

.. table:: **Table 1** Key modules

   +-----------------+-------------------------------------------------------------------------------------+
   | Connection Name | Description                                                                         |
   +=================+=====================================================================================+
   | Manager         | Cluster Manager                                                                     |
   +-----------------+-------------------------------------------------------------------------------------+
   | Manager WS      | WebBrowser                                                                          |
   +-----------------+-------------------------------------------------------------------------------------+
   | Kerberos1       | KrbServer (management plane) service deployed in MRS Manager, that is, OMS Kerberos |
   +-----------------+-------------------------------------------------------------------------------------+
   | Kerberos2       | KrbServer (service plane) service deployed in the cluster                           |
   +-----------------+-------------------------------------------------------------------------------------+
   | LDAP1           | LdapServer (management plane) service deployed in MRS Manager, that is, OMS LDAP    |
   +-----------------+-------------------------------------------------------------------------------------+
   | LDAP2           | LdapServer (service plane) service deployed in the cluster                          |
   +-----------------+-------------------------------------------------------------------------------------+

Data operation mode of Kerberos1 in LDAP: The active and standby instances of LDAP1 and the two standby instances of LDAP2 can be accessed in load balancing mode. Data write operations can be performed only in the active LDAP1 instance. Data read operations can be performed in LDAP1 or LDAP2.

Data operation mode of Kerberos2 in LDAP: Data read operations can be performed in LDAP1 and LDAP2. Data write operations can be performed only in the active LDAP1 instance.

Principle
---------

**Kerberos authentication**


.. figure:: /_static/images/en-us_image_0000001349390661.png
   :alt: **Figure 2** Authentication process

   **Figure 2** Authentication process

**LDAP data read and write**


.. figure:: /_static/images/en-us_image_0000001296750266.png
   :alt: **Figure 3** Data modification process

   **Figure 3** Data modification process

**LDAP data synchronization**

-  OMS LDAP data synchronization before cluster installation


   .. figure:: /_static/images/en-us_image_0000001296590650.png
      :alt: **Figure 4** OMS LDAP data synchronization

      **Figure 4** OMS LDAP data synchronization

   Data synchronization direction before cluster installation: Data is synchronized from the active OMS LDAP to the standby OMS LDAP.

-  LDAP data synchronization after cluster installation


   .. figure:: /_static/images/en-us_image_0000001296270830.png
      :alt: **Figure 5** LDAP data synchronization

      **Figure 5** LDAP data synchronization

   Data synchronization direction after cluster installation: Data is synchronized from the active OMS LDAP to the standby OMS LDAP, standby component LDAP, and standby component LDAP.
