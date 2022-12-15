:original_name: mrs_08_00642.html

.. _mrs_08_00642:

KrbServer and LdapServer Enhanced Open Source Features
======================================================

Enhanced open-source features of KrbServer and LdapServer: intra-cluster service authentication
-----------------------------------------------------------------------------------------------

In an MRS cluster that uses the security mode, mutual access between services is implemented based on the Kerberos security architecture. When a service (such as HDFS) in the cluster is to be started, the corresponding sessionkey (keytab, used for identity authentication of the application) is obtained from Kerberos. If another service (such as YARN) needs to access HDFS and add, delete, modify, or query data in HDFS, the corresponding TGT and ST must be obtained for secure access.

Enhanced Open-Source Features of KrbServer and LdapServer: Application Development Authentication
-------------------------------------------------------------------------------------------------

MRS components provide application development interfaces for customers or upper-layer service product clusters. During application development, a cluster in security mode provides specified application development authentication interfaces to implement application security authentication and access. For example, the UserGroupInformation class provided by the hadoop-common API provides multiple security authentication APIs.

-  **setConfiguration()** is used to obtain related configuration and set parameters such as global variables.
-  **loginUserFromKeytab():** is used to obtain TGT interfaces.

Enhanced Open-Source Features of KrbServer and LdapServer: Cross-System Mutual Trust
------------------------------------------------------------------------------------

MRS provides the mutual trust function between two Managers to implement data read and write operations between systems.
