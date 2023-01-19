:original_name: mrs_01_24091.html

.. _mrs_01_24091:

Savepoint
=========

Savepoints are used to save and restore data of the customized version.

Savepoints provided by Hudi can save different commits so that the cleaner program does not delete them. You can use rollback to restore them later.

Using Hudi CLI to manage savepoints includes:

-  Creating a savepoint

   **savepoint create --commit <commit_time>**

-  Rolling back a savepoint

   **savepoint rollback --savepoint <savepoint_time>**

-  Refreshing savepoints

   **savepoints refresh**

-  Viewing all existing savepoints

   **savepoints show**

.. note::

   MOR tables do not support savepoints.
