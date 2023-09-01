:original_name: mrs_03_1211.html

.. _mrs_03_1211:

How Do I Do If the Time on MRS Nodes Is Incorrect?
==================================================

-  If the time on a node inside the cluster is incorrect, log in to the node and rectify the fault from :ref:`2 <mrs_03_1211__li1924115541119>`.
-  If the time on a node inside the cluster is different from that on a node outside the cluster, log in to the node and rectify the fault from :ref:`1 <mrs_03_1211__li192495514119>`.

#. .. _mrs_03_1211__li192495514119:

   Run the **vi /etc/ntp.conf** command to edit the NTP client configuration file, add the IP addresses of the master node in the MRS cluster, and comment out the IP address of other servers.

   .. code-block::

      server master1_ip prefer
      server master2_ip


   .. figure:: /_static/images/en-us_image_0000001442414233.png
      :alt: **Figure 1** Adding the master node IP addresses

      **Figure 1** Adding the master node IP addresses

#. .. _mrs_03_1211__li1924115541119:

   Run the **service ntpd stop** command to stop the NTP service.

#. Run the **/usr/sbin/ntpdate** *IP address of the active master node* command to manually synchronize time.

#. Run the **service ntpd start** or **systemctl restart ntpd** command to start the NTP service.

#. Run the **ntpstat** command to check the time synchronization result:
