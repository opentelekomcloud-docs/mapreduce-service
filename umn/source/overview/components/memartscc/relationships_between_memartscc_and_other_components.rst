:original_name: mrs_08_0118.html

.. _mrs_08_0118:

Relationships Between MemArtsCC and Other Components
====================================================

OBS
---

OBS provides a new InputStream: OBSMemArtsCCInputStream. This InputStream reads data from the MemArtsCC cluster deployed on the compute side to reduce OBS server pressure and improve data read performance.

MemArtsCC persistently stores data to SSDs on the compute side. OBS interconnects with MemArtsCC to:

#. Improve data access performance in the decoupled storage-compute architecture.

   The local storage of MemArtsCC avoids the cross-network access to hotspot data. This accelerates the data reads of OBS upper-layer applications.

2. Reduce the pressure on the OBS server.

   MemArtsCC stores hotspot data in the compute cluster to reduce the bandwidth pressure of the OBS server.

Spark
-----

Spark reads data from OBS. OBS reads data from MemArtsCC. If data is hit in the local cache, the data is read directly. Otherwise, the data is prefetched.

Hive
----

Hive reads data from OBS. OBS reads data from MemArtsCC. If data is hit in the local cache, the data is read directly. Otherwise, the data is prefetched.

HetuEngine
----------

HetuEngine reads data from OBS. OBS reads data from MemArtsCC. If data is hit in the local cache, the data is read directly. Otherwise, the data is prefetched.
