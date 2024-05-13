:original_name: admin_guide_000315.html

.. _admin_guide_000315:

Security Statement
==================

JDK Usage Statement
-------------------

MRS MRS cluster is a big data cluster that provides users with distributed data analysis and computing capabilities. The built-in JDK of MRS MRS is OpenJDK, which is used in the following scenarios:

-  Platform service running and maintenance
-  Linux client operations, including service submission and application O&M

JDK Risk Description
--------------------

The system performs permission control on the built-in JDK. Only users in the related group of the MRS platform can access the JDK. In addition, the platform is deployed on a customer's intranet. Therefore, the security risk is low.

JDK Hardening
-------------

For details about how to harden the JDK, see "Hardening JDK" in :ref:`Hardening Policies <admin_guide_000272>`.

Public IP Addresses in Hue
--------------------------

Hue uses the test cases of third-party packages, such as **ipadrress**, **requests**, and **Django**, and uses the public IP addresses in the comments of the test cases. However, these public IP addresses are not involved when Hue provides services, and the Hue configuration file does not involve these public IP addresses.
