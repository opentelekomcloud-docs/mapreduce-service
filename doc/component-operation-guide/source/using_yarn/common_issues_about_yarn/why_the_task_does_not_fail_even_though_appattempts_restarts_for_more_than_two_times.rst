:original_name: mrs_01_2081.html

.. _mrs_01_2081:

Why the Task Does Not Fail Even Though AppAttempts Restarts for More Than Two Times?
====================================================================================

Question
--------

Why the task does not fail even though AppAttempts restarts due to failure for more than two times?

Answer
------

During the task execution process, if the **ContainerExitStatus** returns value **ABORTED**, **PREEMPTED**, **DISKS_FAILED**, or **KILLED_BY_RESOURCEMANAGER**, the system will not count it as a failed attempt. Therefore, the task fails only when the AppAttempts fails actually, that is, the return value is not **ABORTED**, **PREEMPTED**, **DISKS_FAILED**, or **KILLED_BY_RESOURCEMANAGER** for two times.
