:original_name: mrs_01_2073.html

.. _mrs_01_2073:

TezUI Cannot Display Tez Task Execution Details
===============================================

Question
--------

After a user logs in to Manager and switches to the Tez web UI, the submitted Tez tasks are not displayed.

Answer
------

The Tez task data displayed on the Tez WebUI requires the support of TimelineServer of Yarn. Ensure that TimelineServer has been enabled and is running properly before the task is submitted.

When setting the Hive execution engine to Tez, you need to set **yarn.timeline-service.enabled** to **true**. For details, see :ref:`Switching the Hive Execution Engine to Tez <mrs_01_1750>`.
