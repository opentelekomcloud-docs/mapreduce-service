:original_name: mrs_01_2075.html

.. _mrs_01_2075:

Yarn Logs Cannot Be Viewed on the TezUI Page
============================================

Question
--------

A user logs in to the Tez web UI and clicks **Logs**, but the Yarn log page fails to be displayed and data cannot be loaded.

Answer
------

Currently, the hostname is used for the access to the Yarn log page from the Tez web UI. Therefore, you need to configure the mapping between the hostname and IP address on the Windows host. Perform the following steps:

Modify the **C:\\Windows\\System32\\drivers\\etc\\hosts** file on the Windows host and add a line indicating the mapping between the host name and IP address, for example, **10.244.224.45 10-044-224-45**. Save the modification and access the host again.
