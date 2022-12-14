:original_name: mrs_01_0982.html

.. _mrs_01_0982:

Optimizing SQL Statements
=========================

Scenario
--------

When SQL statements are executed on Hive, if the **(a&b) or (a&c)** logic exists in the statements, you are advised to change the logic to **a & (b or c)**.

Example
-------

If condition a is **p_partkey = l_partkey**, the statements before optimization are as follows:

.. code-block::

   select
           sum(l_extendedprice* (1 - l_discount)) as revenue
   from
           lineitem,
           part
   where
           (
                   p_partkey = l_partkey
                   and p_brand = 'Brand#32'
                   and p_container in ('SM CASE', 'SM BOX', 'SM PACK', 'SM PKG')
                   and l_quantity >= 7 and l_quantity <= 7 + 10
                   and p_size between 1 and 5
                   and l_shipmode in ('AIR', 'AIR REG')
                   and l_shipinstruct = 'DELIVER IN PERSON'
           )
           or
           (       p_partkey = l_partkey
                   and p_brand = 'Brand#35'
                   and p_container in ('MED BAG', 'MED BOX', 'MED PKG', 'MED PACK')
                   and l_quantity >= 15 and l_quantity <= 15 + 10
                   and p_size between 1 and 10
                   and l_shipmode in ('AIR', 'AIR REG')
                   and l_shipinstruct = 'DELIVER IN PERSON'
           )
           or
           (       p_partkey = l_partkey
                   and p_brand = 'Brand#24'
                   and p_container in ('LG CASE', 'LG BOX', 'LG PACK', 'LG PKG')
                   and l_quantity >= 26 and l_quantity <= 26 + 10
                   and p_size between 1 and 15
                   and l_shipmode in ('AIR', 'AIR REG')
                   and l_shipinstruct = 'DELIVER IN PERSON'
           )

The statements after optimization are as follows:

.. code-block::

   select
           sum(l_extendedprice* (1 - l_discount)) as revenue
   from
           lineitem,
           part
   where   p_partkey = l_partkey and
           ((
                   p_brand = 'Brand#32'
                   and p_container in ('SM CASE', 'SM BOX', 'SM PACK', 'SM PKG')
                   and l_quantity >= 7 and l_quantity <= 7 + 10
                   and p_size between 1 and 5
                   and l_shipmode in ('AIR', 'AIR REG')
                   and l_shipinstruct = 'DELIVER IN PERSON'
           )
           or
           (
                   p_brand = 'Brand#35'
                   and p_container in ('MED BAG', 'MED BOX', 'MED PKG', 'MED PACK')
                   and l_quantity >= 15 and l_quantity <= 15 + 10
                   and p_size between 1 and 10
                   and l_shipmode in ('AIR', 'AIR REG')
                   and l_shipinstruct = 'DELIVER IN PERSON'
           )
           or
           (
                   p_brand = 'Brand#24'
                   and p_container in ('LG CASE', 'LG BOX', 'LG PACK', 'LG PKG')
                   and l_quantity >= 26 and l_quantity <= 26 + 10
                   and p_size between 1 and 15
                   and l_shipmode in ('AIR', 'AIR REG')
                   and l_shipinstruct = 'DELIVER IN PERSON'
           ))
