:original_name: mrs_03_1162.html

.. _mrs_03_1162:

How Do I Configure the knox Memory?
===================================

#. Log in to a Master node of the cluster as user **root**.

#. Run the following command on the Master node to open the **gateway.sh** file:

   **su omm**

   **vim /opt/knox/bin/gateway.sh**

#. Change **APP_MEM_OPTS=""** to **APP_MEM_OPTS="-Xms256m -Xmx768m"**, save the file, and exit.

#. Run the following command on the Master node to restart the knox process:

   **sh /opt/knox/bin/gateway.sh stop**

   **sh /opt/knox/bin/gateway.sh start**

#. Repeat the preceding steps on each Master node.

#. Run the **ps -ef \|grep knox** command to check the configured memory.


   .. figure:: /_static/images/en-us_image_0293101307.png
      :alt: **Figure 1** knox memory

      **Figure 1** knox memory
