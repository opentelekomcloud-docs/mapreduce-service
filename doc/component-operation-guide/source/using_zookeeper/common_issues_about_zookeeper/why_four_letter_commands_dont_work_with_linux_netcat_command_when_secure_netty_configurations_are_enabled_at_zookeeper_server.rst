:original_name: mrs_01_2110.html

.. _mrs_01_2110:

Why Four Letter Commands Don't Work With Linux netcat Command When Secure Netty Configurations Are Enabled at Zookeeper Server?
===============================================================================================================================

Question
--------

Why four letter commands do not work with linux netcat command when secure netty configurations are enabled at Zookeeper server?

For example,

**echo stat \|netcat host port**

Answer
------

Linux **netcat** command does not have option to communicate Zookeeper server securely, so it cannot support Zookeeper four letter commands when secure netty configurations are enabled.

To avoid this problem, user can use below Java API to execute four letter commands.

.. code-block::

   org.apache.zookeeper.client.FourLetterWordMain

For example,

.. code-block::

   String[] args = new String[]{host, port, "stat"};
   org.apache.zookeeper.client.FourLetterWordMain.main(args);

.. note::

   **netcat** command should be used only with non secure netty configuration.
