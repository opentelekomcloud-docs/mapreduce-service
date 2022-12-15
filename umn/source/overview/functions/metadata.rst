:original_name: mrs_08_0075.html

.. _mrs_08_0075:

Metadata
========

MRS provides multiple metadata storage methods. When deploying Hive and Ranger during MRS cluster creation, select one of the following storage modes as required:

-  **Local**: Metadata is stored in the local GaussDB of a cluster. When the cluster is deleted, the metadata is also deleted. To retain the metadata, manually back up the metadata in the database in advance.
-  **Data Connection**: Metadata is stored in the associated PostgreSQL or MySQL database of the RDS service in the same VPC and subnet as the current cluster. When the cluster is terminated, the metadata is not deleted. Multiple MRS clusters can share the metadata.

.. note::

   Hive in MRS 1.9.\ *x* or later allows you to specify a metadata storage method.

   Ranger in MRS 1.9.\ *x* allows metadata to be stored only in the associated MySQL database of the RDS service.
