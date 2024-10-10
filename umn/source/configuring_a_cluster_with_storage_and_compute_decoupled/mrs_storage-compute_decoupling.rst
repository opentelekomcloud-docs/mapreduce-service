:original_name: mrs_01_0467.html

.. _mrs_01_0467:

MRS Storage-Compute Decoupling
==============================

In scenarios that require large storage capacity and elastic compute resources, MRS enables you to store data in OBS and use an MRS cluster for data computing only. In this way, storage and compute are separated.

.. note::

   In the big data decoupled storage-compute scenario, the OBS parallel file system must be used to configure a cluster. Using common object buckets will greatly affect the cluster performance.

Process of using the storage-compute decoupling function:

#. Configure a storage-compute decoupled cluster using either of the following methods (agency is recommended):

   -  Bind an agency of the ECS type to an MRS cluster to access OBS, preventing the AK/SK from being exposed in the configuration file. For details, see :ref:`Configuring a Storage-Compute Decoupled Cluster (Agency) <mrs_01_0768>`.
   -  Configure the AK/SK in an MRS cluster. The AK/SK will be exposed in the configuration file in plaintext. Exercise caution when performing this operation. For details, see :ref:`Configuring a Storage-Compute Decoupled Cluster (AK/SK) <mrs_01_0468>`.
   -  MRS uses the Guardian component to connect to OBS, providing other components with the capabilities of obtaining temporary authentication credentials and fine-grained permission control for accessing OBS. For details, see :ref:`Interconnecting the Guardian Service with OBS <mrs_01_248978>`.

      .. note::

         -  Currently, using Guardian components to connect to OBS is supported only in MRS 3.3.0-LTS or later versions. For details about configurations in clusters of other versions, see :ref:`Interconnecting MRS with OBS Using an Agency <mrs_01_0643>`.
         -  Job submission based on the Guardian storage and compute decoupling management plane depends on JobGateway instead of Executor.

#. Use the cluster.

   After the required permissions for accessing OBS are obtained, components in the MRS cluster can access the corresponding files through the client.

   For details about how to configure components to access OBS, see the following content:

   -  :ref:`Interconnecting MRS with OBS Using an Agency <mrs_01_0643>`
   -  :ref:`Interconnecting Components with OBS Using Guardian <mrs_01_248988>`
