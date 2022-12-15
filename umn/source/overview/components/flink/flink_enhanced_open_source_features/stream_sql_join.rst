:original_name: mrs_08_00348.html

.. _mrs_08_00348:

Stream SQL Join
===============

Enhanced Open Source Feature: Stream SQL Join
---------------------------------------------

Flink's Table API&SQL is an integrated query API for Scala and Java that allows the composition of queries from relational operators such as selection, filter, and join in an intuitive way. For details about Table API&SQL, visit the official website at https://ci.apache.org/projects/flink/flink-docs-release-1.12/dev/table/index.html.

**Introduction to Stream SQL Join**

SQL Join is used to query data based on the relationship between columns in two or more tables. Flink Stream SQL Join allows you to join two streaming tables and query results from them. Queries similar to the following are supported:

.. code-block::

   SELECT o.proctime, o.productId, o.orderId, s.proctime AS shipTime
   FROM Orders AS o
   JOIN Shipments AS s
   ON o.orderId = s.orderId
   AND o.proctime BETWEEN s.proctime AND s.proctime + INTERVAL '1' HOUR;

Currently, Stream SQL Join needs to be performed within a specified window. The join operation for data within the window requires at least one equi-join predicate and a join condition that bounds the time on both sides. Such a condition can be defined by two appropriate range predicates (**<**, **<=**, **>=**, **>**), a **BETWEEN** predicate, or a single equality predicate that compares the same type of time attributes (such as processing time or event time) of both input tables.

The following example will join all orders with their corresponding shipments if the order was shipped four hours after the order was received.

.. code-block::

   SELECT *
   FROM Orders o, Shipments s
   WHERE o.id = s.orderId AND
   o.ordertime BETWEEN s.shiptime - INTERVAL '4' HOUR AND s.shiptime

.. note::

   #. Stream SQL Join supports only inner join.
   #. The **ON** clause should include an equal join condition.
   #. Time attributes support only the processing time and event time.
   #. The window condition supports only the bounded time range, for example, **o.proctime BETWEEN s.proctime - INTERVAL '1' HOUR AND s.proctime + INTERVAL '1' HOUR**. The unbounded range such as **o. proctime > s.proctime** is not supported. The **proctime** attribute of two streams must be included. **o.proctime BETWEEN proctime () AND proctime () + 1** is not supported.
