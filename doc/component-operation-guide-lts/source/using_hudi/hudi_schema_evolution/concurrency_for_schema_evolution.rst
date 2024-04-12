:original_name: mrs_01_24550.html

.. _mrs_01_24550:

Concurrency for Schema Evolution
================================

.. caution::

   When creating a table, you need to set **hoodie.cleaner.policy.failed.writes** to **LAZY**. Otherwise, rollback will be triggered when concurrent submission operations are performed.

DDL Concurrency
---------------

.. table:: **Table 1** Concurrent DDL operations

   ============== === ====== =========== ============== ====
   DDL Operation  add rename change type change comment drop
   ============== === ====== =========== ============== ====
   add            Y   Y      Y           Y              Y
   rename         Y   Y      Y           Y              Y
   change type    Y   Y      Y           Y              Y
   change comment Y   Y      Y           Y              Y
   drop           Y   Y      Y           Y              N
   ============== === ====== =========== ============== ====

.. note::

   When performing DDL operations on the same column concurrently, pay attention to the following:

   -  Multiple drop operations cannot be concurrently performed on the same column. Otherwise, only the first drop operation can be successfully performed and then exception message "java.lang.UnsupportedOperationException: cannot evolution schema implicitly, the column for which the update operation is performed does not exist." is thrown.
   -  When drop, rename, change type, and change comment operations are concurrently performed , drop operations must be executed last. Otherwise, only drop and operations before drop can be performed, and exception message "java.lang.UnsupportedOperationException: cannot evolution schema implicitly, the column for which the update operation is performed does not exist." is thrown when operations after drop are performed.

DDL and DML Concurrency
-----------------------

.. table:: **Table 2** Concurrent DDL and DML operations

   ============== =========== ====== ====== =========
   DDL Operation  insert into update delete set/reset
   ============== =========== ====== ====== =========
   add            Y           Y      Y      Y
   rename         N           N      Y      N
   change type    N           N      Y      N
   change comment Y           Y      Y      Y
   drop           N           N      Y      N
   ============== =========== ====== ====== =========

.. note::

   Exception message "cannot evolution schema implicitly, actions such as rename, delete, and type change were found" is thrown when unsupported DDL or DML operations are performed concurrently.
