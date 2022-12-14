:original_name: mrs_01_2060.html

.. _mrs_01_2060:

Why JRE fatal error after running Spark application multiple times?
===================================================================

Question
--------

Why JRE fatal error after running Spark application multiple times?

Answer
------

When you run Spark application multiple times, JRE fatal error occurs and this is due to the problem with the Linux Kernel.

To resolve this issue, upgrade the **kernel version to 4.13.9-2.ge7d7106-default**.
