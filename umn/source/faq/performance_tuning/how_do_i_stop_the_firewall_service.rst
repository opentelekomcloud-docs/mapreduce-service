:original_name: mrs_03_1072.html

.. _mrs_03_1072:

How Do I Stop the Firewall Service?
===================================

#. Log in to each node of a cluster as user **root**.

#. Check whether the firewall service is started.

   For example, to check the firewall status on EulerOS, run the **systemctl status firewalld.service** command.

#. Stop the firewall service.

   For example, to stop the firewall service on EulerOS, run the **systemctl stop firewalld.service** command.
