:original_name: mrs_01_1648.html

.. _mrs_01_1648:

Why "java.lang.UnsatisfiedLinkError: Permission denied" exception thrown while starting HBase shell?
====================================================================================================

Question
--------

Why "java.lang.UnsatisfiedLinkError: Permission denied" exception thrown while starting HBase shell?

Answer
------

During HBase shell execution JRuby create temporary files under **java.io.tmpdir** path and default value of **java.io.tmpdir** is **/tmp**. If NOEXEC permission is set to /tmp directory then HBase shell start will fail with "java.lang.UnsatisfiedLinkError: Permission denied" exception.

So "java.io.tmpdir" must be set to a different path in HBASE_OPTS/CLIENT_GC_OPTS if NOEXEC is set to /tmp directory.
