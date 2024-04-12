:original_name: mrs_01_24783.html

.. _mrs_01_24783:

ARCHIVELOG
==========

.. note::

   This section applies only to MRS 3.2.0 or later.

Function
--------

Archives instants on the Timeline based on configurations and deletes archived instants from the Timeline to reduce the operation pressure on the Timeline.

Syntax
------

**RUN ARCHIVELOG ON** tableIdentifier;

**RUN ARCHIVELOG ON** tablelocation;

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

   run archivelog on h1;
   run archivelog on "/tmp/hudi/h1";

Precautions
-----------

-  Only instants that are not cleaned can be archived.
-  No matter whether the compaction operation is performed, at least *x* (*x* indicates the value of **hoodie.compact.inline.max.delta.commits**) instants are retained and not archived to ensure that there are enough instants to trigger the compaction schedule.

System Response
---------------

You can view command execution results in the driver log or on the client.
