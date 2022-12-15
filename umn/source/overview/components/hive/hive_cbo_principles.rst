:original_name: mrs_08_00112.html

.. _mrs_08_00112:

Hive CBO Principles
===================


Hive CBO Principles
-------------------

CBO is short for Cost-Based Optimization.

It will optimize the following:

During compilation, the CBO calculates the most efficient join sequence based on tables and query conditions involved in query statements to reduce time and resources required for query.

In Hive, the CBO is implemented as follows:

Hive uses open-source component Apache Calcite to implement the CBO. SQL statements are first converted into Hive Abstract Syntax Trees (ASTs) and then into RelNodes that can be identified by Calcite. After Calcite adjusts the join sequence in RelNodes, RelNodes are converted into ASTs by Hive to continue the logical and physical optimization. :ref:`Figure 1 <mrs_08_00112__fig567676115845>` shows the working flow.

.. _mrs_08_00112__fig567676115845:

.. figure:: /_static/images/en-us_image_0000001349390693.png
   :alt: **Figure 1** CBO Implementation process

   **Figure 1** CBO Implementation process

Calcite adjusts the join sequence as follows:

#. A table is selected as the first table from the tables to be joined.
#. The second and third tables are selected based on the cost. In this way, multiple different execution plans are obtained.
#. A plan with the minimum costs is calculated and serves as the final sequence.

The cost calculation method is as follows:

In the current version, costs are measured based on the number of data entries after joining. Fewer data entries mean less cost. The number of joined data entries depends on the selection rate of joined tables. The number of data entries in a table is obtained based on the table-level statistics.

The number of data entries in a table after filtering is estimated based on the column-level statistics, including the maximum values (max), minimum values (min), and Number of Distinct Values (NDV).

For example, there is a table **table_a** whose total number of data records is 1,000,000 and NDV is 50. The query conditions are as follows:

.. code-block::

   Select * from table_a where colum_a='value1';

The estimated number of queried data entries is: 1,000,000 x 1/50 = 20,000. The selection rate is 2%.

The following takes the TPC-DS Q3 as an example to describe how the CBO adjusts the join sequence:

.. code-block::

   select
       dt.d_year,
       item.i_brand_id brand_id,
       item.i_brand brand,
       sum(ss_ext_sales_price) sum_agg
   from
       date_dim dt,
       store_sales,
       item
   where
       dt.d_date_sk = store_sales.ss_sold_date_sk
       and store_sales.ss_item_sk = item.i_item_sk
       and item.i_manufact_id = 436
       and dt.d_moy = 12
   group by dt.d_year , item.i_brand , item.i_brand_id
   order by dt.d_year , sum_agg desc , brand_id
   limit 10;

Statement explanation: This statement indicates that inner join is performed for three tables: table **store_sales** is a fact table with about 2,900,000,000 data entries, table **date_dim** is a dimension table with about 73,000 data entries, and table **item** is a dimension table with about 18,000 data entries. Each table has filtering conditions. :ref:`Figure 2 <mrs_08_00112__fig27230352161945>` shows the join relationship.

.. _mrs_08_00112__fig27230352161945:

.. figure:: /_static/images/en-us_image_0000001349309981.png
   :alt: **Figure 2** Join relationship

   **Figure 2** Join relationship

The CBO must first select the tables that bring the best filtering effect for joining.

By analyzing min, max, NDV, and the number of data entries, the CBO estimates the selection rates of different dimension tables, as shown in :ref:`Table 1 <mrs_08_00112__table21230583162227>`.

.. _mrs_08_00112__table21230583162227:

.. table:: **Table 1** Data filtering

   +----------+---------------------------------+----------------------------------------+----------------+
   | Table    | Number of Original Data Entries | Number of Data Entries After Filtering | Selection Rate |
   +==========+=================================+========================================+================+
   | date_dim | 73,000                          | 6,200                                  | 8.5%           |
   +----------+---------------------------------+----------------------------------------+----------------+
   | item     | 18,000                          | 19                                     | 0.1%           |
   +----------+---------------------------------+----------------------------------------+----------------+

The selection rate can be estimated as follows: Selection rate = Number of data entries after filtering/Number of original data entries

As shown in the preceding table, the **item** table has a better filtering effect. Therefore, the CBO joins the **item** table first before joining the **date_dim** table.

:ref:`Figure 3 <mrs_08_00112__fig46862216163921>` shows the join process when the CBO is disabled.

.. _mrs_08_00112__fig46862216163921:

.. figure:: /_static/images/en-us_image_0000001296590682.png
   :alt: **Figure 3** Join process when the CBO is disabled

   **Figure 3** Join process when the CBO is disabled

:ref:`Figure 4 <mrs_08_00112__fig47832930164032>` shows the join process when the CBO is enabled.

.. _mrs_08_00112__fig47832930164032:

.. figure:: /_static/images/en-us_image_0000001349190397.png
   :alt: **Figure 4** Join process when the CBO is enabled

   **Figure 4** Join process when the CBO is enabled

After the CBO is enabled, the number of intermediate data entries is reduced from 495,000,000 to 2,900,000 and thus the execution time can be remarkably reduced.
