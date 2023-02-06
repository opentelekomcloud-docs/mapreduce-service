:original_name: mrs_01_1695.html

.. _mrs_01_1695:

Why Does the Distcp Command Fail in the Secure Cluster, Causing an Exception?
=============================================================================

Question
--------

Why distcp command fails in the secure cluster with the following error displayed?

Client side exception

.. code-block::

   Invalid arguments: Unexpected end of file from server

Server side exception

.. code-block::

   javax.net.ssl.SSLException: Unrecognized SSL message, plaintext connection?

Answer
------

The preceding error may occur if **webhdfs://** is used in the distcp command. The reason is that the big data cluster uses the HTTPS mechanism, that is, **dfs.http.policy** is set to **HTTPS_ONLY** in **core-site.xml** file. To avoid the error, replace **webhdfs://** with **swebhdfs://** in the file.

For example:

**./hadoop distcp** **swebhdfs://IP:PORT/testfile hdfs://IP:PORT/testfile1**
