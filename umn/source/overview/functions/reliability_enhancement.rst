:original_name: mrs_08_0045.html

.. _mrs_08_0045:

Reliability Enhancement
=======================

Based on Apache Hadoop open source software, MRS optimizes and improves the reliability and performance of main service components.

System Reliability
------------------

-  HA for all management nodes

   In the Hadoop open source version, data and compute nodes are managed in a distributed system, in which a single point of failure (SPOF) does not affect the operation of the entire system. However, a SPOF may occur on management nodes running in centralized mode, which becomes the weakness of the overall system reliability.

   MRS provides similar double-node mechanisms for all management nodes of the service components, such as Manager, HDFS NameNodes, HiveServers, HBase HMasters, Yarn ResourceManagers, KerberosServers, and LdapServers. All of them are deployed in active/standby mode or configured with load sharing, effectively preventing SPOFs from affecting system reliability.

-  Reliability guarantee in case of exceptions

   By reliability analysis, the following measures to handle software and hardware exceptions are provided to improve the system reliability:

   -  After power supply is restored, services are running properly regardless of a power failure of a single node or the whole cluster, ensuring data reliability in case of unexpected power failures. Key data will not be lost unless the hard disk is damaged.
   -  Health status checks and fault handling of the hard disk do not affect services.
   -  The file system faults can be automatically handled, and affected services can be automatically restored.
   -  The process and node faults can be automatically handled, and affected services can be automatically restored.
   -  The network faults can be automatically handled, and affected services can be automatically restored.

-  Data backup and restoration

   MRS provides full backup, incremental backup, and restoration functions based on service requirements, preventing the impact of data loss and damages on services and ensuring fast system restoration in case of exceptions.

   -  Automatic backup

      MRS provides automatic backup for data on Manager. Based on the customized backup policy, data on clusters, including LdapServer and DBService data, can be automatically backed up.

   -  Manual backup

      You can also manually back up data of the cluster management system before the capacity expansion and patch installation to recover the cluster management system functions upon faults.

      To improve the system reliability, data on Manager and HBase is backed up to a third-party server manually.

Node Reliability
----------------

-  OS health status monitoring

   MRS periodically collects OS hardware resource usage data, including usage of CPUs, memory, hard disks, and network resources.

-  Process health status monitoring

   MRS checks the status of service instances and health indicators of service instance processes, enabling you to know the health status of processes in a timely manner.

-  Automatic disk troubleshooting

   MRS is enhanced based on the open source version. It can monitor the status of hardware and file systems on all nodes. If an exception occurs, the corresponding partitions will be removed from the storage pool. If a disk is faulty and replaced, a new hard disk will be added for running services. In this case, maintenance operations are simplified. Replacement of faulty disks can be completed online. In addition, users can set hot backup disks to reduce the faulty disk restoration time and improve the system reliability.

-  LVM configuration for node disks

   MRS allows you to configure Logic Volume Management (LVM) to plan multiple disks as a logical volume group. Configuring LVM can avoid uneven usage of disks. It is especially important to ensure even usage of disks on components that can use multiple disk capabilities, such as HDFS and Kafka. In addition, LVM supports disk capacity expansion without re-attaching, preventing service interruption.

Data Reliability
----------------

MRS can use the anti-affinity node groups and placement group capabilities provided by ECS and the rack awareness capability of Hadoop to redundantly distribute data to multiple physical host machines, preventing data loss caused by physical hardware failures.
