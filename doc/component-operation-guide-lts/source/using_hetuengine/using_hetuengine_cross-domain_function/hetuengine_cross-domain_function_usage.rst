:original_name: mrs_01_2335.html

.. _mrs_01_2335:

HetuEngine Cross-Domain Function Usage
======================================

#. Open the data source in the local domain. You can create a virtual schema to shield the real schema information and instance information of the physical data source in the local domain from remote access requests. The remote end can use the virtual schema name to access the data source in the local domain.

   .. code-block::

      CREATE VIRTUAL SCHEMA hive01.vschema01 WITH (
        catalog = 'hive01',
        schema = 'ins1'
      );

#. Register the data source of the HetuEngine type on the remote HetuEngine and add the local domain HetuEngine by referring to :ref:`Configuring a HetuEngine Data Source <mrs_01_1719>`.

#. Use cross-domain collaborative analysis.

   .. code-block::

      // 1. Open the hive1.ins2 data source on the remote HetuEngine.
      CREATE VIRTUAL SCHEMA hive1.vins2 WITH (
        catalog = 'hive1',
        schema = 'ins2'
      );

      // 2. Register three types of data sources, including Hive, GaussDB A, and HetuEngine, on HetuEngine in the local domain.
      hetuengine> show catalogs;
        Catalog
      ----------
      dws
      hetuengine_dc
      hive
      hive_dg
      system
      systemremote
      (6 rows)

      // 3. Perform cross-source collaborative analysis on HetuEngine in the local domain.
      select * from hive_dg.schema1.table1 t1 join hetuengine_dc.vins2.table3 t2 join dws.schema02.table4 t3 on t1.name = t2.item and t2.id = t3.cardNo;
