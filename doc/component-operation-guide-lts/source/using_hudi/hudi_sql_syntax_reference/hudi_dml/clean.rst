:original_name: mrs_01_24801.html

.. _mrs_01_24801:

CLEAN
=====

.. note::

   This section applies only to MRS 3.2.0 or later.

Function
--------

Cleans instants on the Timeline based on configurations and deletes historical version files to reduce the data storage and read/write pressure of Hudi tables.

Syntax
------

**RUN CLEAN ON** tableIdentifier;

**RUN CLEAN ON** tablelocation;

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   =============== ==============================
   Parameter       Description
   =============== ==============================
   tableIdentifier Name of the Hudi table
   tablelocation   Storage path of the Hudi table
   =============== ==============================

Example
-------

.. code-block::

   run clean on h1;
   run clean on "/tmp/hudi/h1";

Precautions
-----------

Only the table owner can perform the clean operation on a table.

To modify the default cleaning parameters, run set commands to configure the parameters such as the number of commits to be retained.

System Response
---------------

You can view command execution results in the driver log or on the client.
