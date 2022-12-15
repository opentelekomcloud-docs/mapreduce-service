:original_name: mrs_03_1156.html

.. _mrs_03_1156:

Why Cannot I Refresh the Dynamic Resource Plan Page on MRS Tenant Tab?
======================================================================

#. Log in to the Master1 and Master2 nodes as user **root**.

#. Run the **ps -ef \|grep aos** command to check the AOS process ID.

#. Run the **kill -9** *AOS process ID* command to end the AOS process.

#. Wait until the AOS process is automatically restarted.

   You can run the **ps -ef \|grep aos** command to check whether the AOS process restarts successfully. If the process exists, the restart is successful and the **Dynamic Resource Plan** page will be refreshed. If the process does not exist, retry later.
