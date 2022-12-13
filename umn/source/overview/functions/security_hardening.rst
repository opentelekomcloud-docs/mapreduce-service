:original_name: mrs_08_0043.html

.. _mrs_08_0043:

Security Hardening
==================

MRS is a platform for massive data management and analysis and has high security. MRS protects user data and service running from the following aspects:

-  Network isolation

   The entire system is deployed in a VPC on the public cloud to provide an isolated network environment and ensure service and management security of the cluster. By combining the subnet division, route control, and security group functions of VPC, MRS provides a secure and reliable isolated network environment.

-  Resource isolation

   MRS supports resource deployment and isolation of physical resources in dedicated zones. You can flexibly combine computing and storage resources, such as dedicated computing resources + shared storage resources, shared computing resources + dedicated storage resources, and dedicated computing resources + dedicated storage resources.

-  Host security

   MRS can be integrated with public cloud security services, including Vulnerability Scan Service (VSS), Host Security Service (HSS), Web Application Firewall (WAF), Cloud Bastion Host (CBH), and Web Tamper Protection (WTP). The following measures are provided to improve security of the OS and ports:

   -  Security hardening of OS kernels
   -  OS patch update
   -  OS permission control
   -  OS port management
   -  OS protocol and port attack defense

-  Application security

   The following measures are used to ensure normal running of big data services:

   -  Identification and authentication
   -  Web application security
   -  Access control
   -  Audit security
   -  Password security

-  Data security

   The following measures are provided to ensure the confidentiality, integrity, and availability of massive amounts of user data:

   -  Disaster recovery: MRS supports data backup to OBS and cross-region high reliability.
   -  Backup: MRS supports backup of DBService, NameNode, and LDAP metadata and backup of HDFS and HBase service data.

-  Data integrity

   Data is verified to ensure its integrity during storage and transmission.

   -  CRC32C is used by default to verify the correctness of user data stored in HDFS.
   -  DataNodes of HDFS store the verified data. If the data transmitted from a client is abnormal (incomplete), DataNodes report the abnormality to the client, and the client rewrites the data.
   -  The client checks data integrity when reading data from a DataNode. If the data is incomplete, the client will read data from another DataNode.

-  Data confidentiality

   Based on Apache Hadoop, the distributed file system of MRS supports encrypted storage of files to prevent sensitive data from being stored in plaintext, improving data security. Applications need only to encrypt specified sensitive data. Services are not affected during the encryption process. Based on file system data encryption, Hive provides table-level encryption and HBase provides column family-level encryption. Sensitive data can be encrypted and stored after you specify an encryption algorithm during table creation.

   Encrypted storage and access control of data are used to ensure user data security.

   -  HBase stores service data to the HDFS after compression. Users can configure the AES and SMS4 encryption algorithm to encrypt data.
   -  All the components allow access permissions to be set for local data directories. Unauthorized users are not allowed to access data.
   -  All cluster user information is stored in ciphertext.

-  Security authentication

   -  Uses a unified user- and role-based authentication system as well as an account- and role-based access control (RBAC) model to centrally control user permissions and batch manage user authorization.
   -  Employs Lightweight Directory Access Protocol (LDAP) as an account management system and performs the Kerberos authentication on accounts.
   -  Provides the single sign-on (SSO) function that centrally manages and authenticates MRS system and component users.
   -  Audits users who have logged in to Manager.
