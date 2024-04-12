:original_name: mrs_01_24798.html

.. _mrs_01_24798:

Configuring Intelligent Materialized Views
==========================================

Overview
--------

HetuEngine intelligent materialized views provide intelligent precalculation and cache acceleration. The HetuEngine QAS role can automatically extract historical SQL statements for analysis and learning, and automatically generate candidate SQL statements for high-value materialized views based on the revenue maximization principle. In practice, HetuEngine administrators can enable automatic creation and refresh of materialized views by configuring maintenance instances. Service users can configure client sessions to implement automatic rewriting and acceleration based on automatically created materialized views.

This capability significantly simplifies the use of materialized views and accelerates analysis without interrupting services. HetuEngine administrators can intelligently accelerate high-frequency SQL services by using a small amount of compute and storage resources. In addition, this capability reduces the overall load (such as CPU, memory, and I/O) of the data platform and improves system stability.

The intelligent materialized view provides the following functions:

-  Automatic recommendation of materialized views
-  Automatic creation of materialized views
-  Automatic refresh of materialized views
-  Automatic deletion of materialized views

Prerequisites
-------------

The cluster is running properly and at least one QAS instance has been installed.

Application Process
-------------------


.. figure:: /_static/images/en-us_image_0000001533639950.png
   :alt: **Figure 1** Application process of HetuEngine intelligent materialized views

   **Figure 1** Application process of HetuEngine intelligent materialized views

.. table:: **Table 1** Process description

   +-------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Step                                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                      | Reference                                                                                                         |
   +=======================================================+==================================================================================================================================================================================================================================================================================================================================================================================================================================+===================================================================================================================+
   | Enable the materialized view recommendation function. | After this function is enabled, QAS instances automatically recommend SQL statements of high-value materialized views based on users' SQL execution records. You can view the recommended materialized view statements on the materialized view recommendation page on the HSConsole. For details, see :ref:`Viewing Materialized View Recommendation Results <mrs_01_24776__en-us_topic_0000001521080921_section051233712276>`. | :ref:`Enabling Materialized View Recommendation <mrs_01_24776__en-us_topic_0000001521080921_section109434212018>` |
   +-------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Configure a maintenance instance.                     | After a compute instance is set as a maintenance instance, the maintenance instance automatically creates, refreshes, and deletes the materialized view SQL statements recommended by the materialized view recommendation function. You can view the generated automatic task records on the HetuEngine automation task page. For details, see :ref:`Viewing Automatic Tasks of Materialized Views <mrs_01_24505>`.             | :ref:`Configuring a HetuEngine Maintenance Instance <mrs_01_24535>`                                               |
   +-------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Enable rewriting of materialized views.               | After rewriting is enabled for materialized views, HetuEngine determines whether the materialized view rewriting requirements are met based on the SQL statements entered by users and converts queries or subqueries that match materialized views into materialized views, avoiding repeated data calculation.                                                                                                                 | :ref:`Configuring Rewriting of Materialized Views <mrs_01_24543>`                                                 |
   +-------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
