:original_name: mrs_01_1466.html

.. _mrs_01_1466:

Why Data loading Fails During off heap?
=======================================

Question
--------

Why Data Loading fails during off heap?

Answer
------

YARN Resource Manager will consider (Java heap memory + **spark.yarn.am.memoryOverhead**) as memory limit, so during the off heap, the memory can exceed this limit. So you need to increase the memory by increasing the value of the parameter **spark.yarn.am.memoryOverhead**.
