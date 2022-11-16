:original_name: mrs_01_9005.html

.. _mrs_01_9005:

ECS Specifications Used by MRS
==============================

MRS uses ECSs of the following types in different application scenarios.

-  General computing (S1)
-  General computing (S3)
-  General computing (C2)
-  General computing-plus (C3)
-  General computing-plus (C4)
-  General computing-plus (C6)
-  Disk-intensive (D1)
-  Disk-intensive (D2)
-  High-performance computing (H1)
-  Memory-optimized (M3)
-  Memory-optimized (M4)

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

.. table:: **Table 1** S1 ECS specifications

   ==== ===== =========== ==================== ===================
   Type vCPUs Memory (GB) Flavor               Virtualization Type
   ==== ===== =========== ==================== ===================
   S1   4     16          s1.xlarge.linux.mrs  XEN
   \    16    64          s1.4xlarge.linux.mrs XEN
   \    32    128         s1.8xlarge.linux.mrs XEN
   ==== ===== =========== ==================== ===================

.. table:: **Table 2** S3 ECS specifications

   ==== ===== =========== ====================== ===================
   Type vCPUs Memory (GB) Flavor                 Virtualization Type
   ==== ===== =========== ====================== ===================
   S3   4     8           s3.xlarge.2.linux.mrs  XEN
   \    4     16          s3.xlarge.4.linux.mrs  XEN
   \    8     16          s3.2xlarge.2.linux.mrs XEN
   \    8     32          s3.2xlarge.4.linux.mrs XEN
   \    16    32          s3.4xlarge.2.linux.mrs XEN
   ==== ===== =========== ====================== ===================

.. table:: **Table 3** C2 ECS specifications

   ==== ===== =========== ==================== ===================
   Type vCPUs Memory (GB) Flavor               Virtualization Type
   ==== ===== =========== ==================== ===================
   C2   8     16          c2.2xlarge.linux.mrs KVM
   \    16    32          c2.4xlarge.linux.mrs KVM
   ==== ===== =========== ==================== ===================

.. table:: **Table 4** General computing-plus (C3) ECS specifications

   ==== ===== =========== ======================= ===================
   Type vCPUs Memory (GB) Flavor                  Virtualization Type
   ==== ===== =========== ======================= ===================
   C3   8     16          c3.2xlarge.2.linux.mrs  KVM
   \    4     16          c3.xlarge.4.linux.mrs   KVM
   \    8     32          c3.2xlarge.4.linux.mrs  KVM
   \    16    32          c3.4xlarge.2.linux.mrs  KVM
   \    16    64          c3.4xlarge.4.linux.mrs  KVM
   \    32    128         c3.8xlarge.4.linux.mrs  KVM
   \    60    256         c3.15xlarge.4.linux.mrs KVM
   ==== ===== =========== ======================= ===================

.. table:: **Table 5** C4 ECS specifications

   ==== ===== =========== ======================= ===================
   Type vCPUs Memory (GB) Flavor                  Virtualization Type
   ==== ===== =========== ======================= ===================
   C4   4     16          c4.xlarge.4.linux.mrs   KVM
   \    8     16          c4.2xlarge.2.linux.mrs  KVM
   \    8     32          c4.2xlarge.4.linux.mrs  KVM
   \    16    32          c4.4xlarge.2.linux.mrs  KVM
   \    16    64          c4.4xlarge.4.linux.mrs  KVM
   \    32    64          c4.8xlarge.2.linux.mrs  KVM
   \    32    128         c4.8xlarge.4.linux.mrs  KVM
   \    64    256         c4.16xlarge.4.linux.mrs KVM
   ==== ===== =========== ======================= ===================

.. table:: **Table 6** C6 ECS specifications

   ==== ===== =========== ======================= ===================
   Type vCPUs Memory (GB) Flavor                  Virtualization Type
   ==== ===== =========== ======================= ===================
   c6   8     32          c6.2xlarge.4.linux.mrs  KVM
   \    16    64          c6.4xlarge.4.linux.mrs  KVM
   \    32    64          c6.8xlarge.2.linux.mrs  KVM
   \    32    128         c6.8xlarge.4.linux.mrs  KVM
   \    64    128         c6.16xlarge.2.linux.mrs KVM
   \    64    256         c6.16xlarge.4.linux.mrs KVM
   ==== ===== =========== ======================= ===================

.. table:: **Table 7** D1 ECS specifications

   +---------+---------+-------------+-------------------------+---------------------+-----------------+------------------------------------------+
   | Type    | vCPUs   | Memory (GB) | Flavor                  | Virtualization Type | Local Disk (GB) | Hardware                                 |
   +=========+=========+=============+=========================+=====================+=================+==========================================+
   | D1      | 44      | 3232        | d1.xlarge.mrslinux.mrs  | KVM                 | 3x1800          | CPU: Intel® Xeon® Gold 6151 Processor v5 |
   |         |         |             |                         |                     |                 |                                          |
   |         |         |             |                         |                     |                 | Memory: 20 x 32 GB                       |
   +---------+---------+-------------+-------------------------+---------------------+-----------------+------------------------------------------+
   |         | 88      | 6464        | d1.2xlarge.mrslinux.mrs | KVM                 | 6x1800          |                                          |
   +---------+---------+-------------+-------------------------+---------------------+-----------------+------------------------------------------+
   |         | 16      | 128         | d1.4xlarge.linux.mrs    | KVM                 | 12x1800         |                                          |
   +---------+---------+-------------+-------------------------+---------------------+-----------------+------------------------------------------+
   |         | 36      | 256         | d1.8xlarge.linux.mrs    | KVM                 | 24x1800         |                                          |
   +---------+---------+-------------+-------------------------+---------------------+-----------------+------------------------------------------+

.. table:: **Table 8** D2 ECS specifications

   +---------+---------+-------------+------------------------+---------------------+-----------------+------------------------------------------+
   | Type    | vCPUs   | Memory (GB) | Flavor                 | Virtualization Type | Local Disk (GB) | Hardware                                 |
   +=========+=========+=============+========================+=====================+=================+==========================================+
   | D2      | 4       | 32          | d2.xlarge.8.linux.mrs  | KVM                 | 2x1800          | CPU: Intel® Xeon® Gold 6151 Processor v5 |
   |         |         |             |                        |                     |                 |                                          |
   |         |         |             |                        |                     |                 | Memory: 20 x 32 GB                       |
   +---------+---------+-------------+------------------------+---------------------+-----------------+------------------------------------------+
   |         | 8       | 64          | d2.2xlarge.8.linux.mrs | KVM                 | 4x1800          |                                          |
   +---------+---------+-------------+------------------------+---------------------+-----------------+------------------------------------------+
   |         | 16      | 128         | d2.4xlarge.8.linux.mrs | KVM                 | 8x1800          |                                          |
   +---------+---------+-------------+------------------------+---------------------+-----------------+------------------------------------------+
   |         | 32      | 256         | d2.8xlarge.8.linux.mrs | KVM                 | 16x1800         |                                          |
   +---------+---------+-------------+------------------------+---------------------+-----------------+------------------------------------------+

.. table:: **Table 9** H1 ECS specifications

   ==== ===== =========== ====================== ===================
   Type vCPUs Memory (GB) Flavor                 Virtualization Type
   ==== ===== =========== ====================== ===================
   H1   8     32          h1.2xlarge.4.linux.mrs KVM
   \    16    64          h1.4xlarge.4.linux.mrs KVM
   \    32    128         h1.8xlarge.4.linux.mrs KVM
   ==== ===== =========== ====================== ===================

.. table:: **Table 10** M3 ECS specifications

   ==== ===== =========== ====================== ===================
   Type vCPUs Memory (GB) Flavor                 Virtualization Type
   ==== ===== =========== ====================== ===================
   M3   8     64          m3.2xlarge.8.linux.mrs KVM
   \    16    128         m3.4xlarge.8.linux.mrs KVM
   \    32    256         m3.8xlarge.8.linux.mrs KVM
   ==== ===== =========== ====================== ===================

.. table:: **Table 11** M4 ECS specifications

   ==== ===== =========== ======================= ===================
   Type vCPUs Memory (GB) Flavor                  Virtualization Type
   ==== ===== =========== ======================= ===================
   M4   8     64          m4.2xlarge.8.linux.mrs  KVM
   \    16    128         m4.4xlarge.8.linux.mrs  KVM
   \    32    256         m4.8xlarge.8.linux.mrs  KVM
   \    64    512         m4.16xlarge.8.linux.mrs KVM
   ==== ===== =========== ======================= ===================
