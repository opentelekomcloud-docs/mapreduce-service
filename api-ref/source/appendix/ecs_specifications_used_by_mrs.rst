:original_name: mrs_01_9005.html

.. _mrs_01_9005:

ECS Specifications Used by MRS
==============================

MRS uses ECSs of the following types in different application scenarios.

.. note::

   The ECS specifications available on MRS console vary by cluster version.

-  General computing (S2)
-  General computing (S3)
-  General computing-plus (C3)
-  General computing-plus (C4)
-  Disk-intensive (D2)

ECS Flavor Naming Rules
-----------------------

AB.C.D

Example: m3.8xlarge.8

In the preceding flavor:

-  **A** specifies the ECS type. For example, **s** indicates a general-purpose ECS, **c** a computing ECS, and **m** a memory-optimized ECS.
-  **B** specifies the type ID. For example, the **1** in **s1** indicates a general-purpose first-generation ECS, and the **2** in **s2** indicates a general-purpose second-generation ECS.
-  **C** specifies a flavor size and can be any of the following options: medium, large, and xlarge.
-  **D** specifies the ratio of memory to vCPUs expressed in a digit. For example, value **4** indicates that the ratio of memory to vCPUs is 4.

Specifications
--------------

.. table:: **Table 1** S2 ECS specifications

   ==== ===== =========== ====================== ===================
   Type vCPUs Memory (GB) Flavor                 Virtualization Type
   ==== ===== =========== ====================== ===================
   S2   16    32          s2.4xlarge.2.linux.mrs XEN
   ==== ===== =========== ====================== ===================

.. table:: **Table 2** S3 ECS specifications

   ==== ===== =========== ====================== ===================
   Type vCPUs Memory (GB) Flavor                 Virtualization Type
   ==== ===== =========== ====================== ===================
   S3   16    32          s3.4xlarge.2.linux.mrs XEN
   ==== ===== =========== ====================== ===================

.. table:: **Table 3** General computing-plus (C3) ECS specifications

   ==== ===== =========== ====================== ===================
   Type vCPUs Memory (GB) Flavor                 Virtualization Type
   ==== ===== =========== ====================== ===================
   C3   16    32          c3.4xlarge.2.linux.mrs KVM
   ==== ===== =========== ====================== ===================

.. table:: **Table 4** C4 ECS specifications

   ==== ===== =========== ====================== ===================
   Type vCPUs Memory (GB) Flavor                 Virtualization Type
   ==== ===== =========== ====================== ===================
   C4   4     16          c4.xlarge.4.linux.mrs  KVM
   \    16    64          c4.4xlarge.4.linux.mrs KVM
   \    32    64          c4.8xlarge.2.linux.mrs KVM
   ==== ===== =========== ====================== ===================

.. table:: **Table 5** D2 ECS specifications

   +---------+---------+-------------+------------------------+---------------------+-----------------+------------------------------------------+
   | Type    | vCPUs   | Memory (GB) | Flavor                 | Virtualization Type | Local Disk (GB) | Hardware                                 |
   +=========+=========+=============+========================+=====================+=================+==========================================+
   | D2      | 16      | 128         | d2.4xlarge.8.linux.mrs | KVM                 | 8x1675          | CPU: Intel® Xeon® Gold 6151 Processor v5 |
   |         |         |             |                        |                     |                 |                                          |
   |         |         |             |                        |                     |                 | Memory: 20 x 32 GB                       |
   +---------+---------+-------------+------------------------+---------------------+-----------------+------------------------------------------+
   |         | 24      | 192         | d2.6xlarge.8.linux.mrs | KVM                 | 12x1675         |                                          |
   +---------+---------+-------------+------------------------+---------------------+-----------------+------------------------------------------+
   |         | 32      | 256         | d2.8xlarge.8.linux.mrs | KVM                 | 16x1675         |                                          |
   +---------+---------+-------------+------------------------+---------------------+-----------------+------------------------------------------+
