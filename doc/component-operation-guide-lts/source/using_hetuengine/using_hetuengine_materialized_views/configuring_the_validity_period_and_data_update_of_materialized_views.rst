:original_name: mrs_01_24546.html

.. _mrs_01_24546:

Configuring the Validity Period and Data Update of Materialized Views
=====================================================================

Validity Period of Materialized Views
-------------------------------------

The **mv_validity** field for creating a materialized view indicates the validity period of the materialized view. HetuEngine allows you to rewrite the SQL statements using only the materialized views within the validity period.

Refreshing Materialized View Data
---------------------------------

If data needs to be updated periodically, you can use either of the following methods to periodically refresh the materialized views:

-  Manually refreshing a materialized view

   Run the **refresh materialized view** *<mv name>* command on the HetuEngine client by referring to HetuEngine, or run the **refresh materialized view** *<mv name>* command using JDBC in the service program to manually update the database.

-  Automatically refreshing a materialized view

   Use **create materialized view** to create a materialized view that can be automatically refreshed.

   .. note::

      -  To enable the automatic refresh capability of the materialized views, you must set a computing instance as the maintenance instance must exist. For details, see :ref:`Configuring a HetuEngine Maintenance Instance <mrs_01_24535>`.
      -  If there are too many materialized views, some materialized views may expire due to too long waiting time.
      -  The automatic refresh function does not automatically refresh materialized views in the **disable** status.
