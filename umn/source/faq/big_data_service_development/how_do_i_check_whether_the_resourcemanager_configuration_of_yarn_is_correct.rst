:original_name: mrs_03_1163.html

.. _mrs_03_1163:

How Do I Check Whether the ResourceManager Configuration of Yarn Is Correct?
============================================================================

#. .. _mrs_03_1163__li92876413199:

   Log in to MRS Manager and choose **Services** > **Yarn** > **Instance**.

#. Synchronize the configuration between the two ResourceManager nodes.Perform the following steps on each ResourceManager node:Click the name of the ResourceManager node, and choose **More** > **Synchronize Configuration**.In the dialog box displayed, deselect **Restart services or instances whose configurations have expired** and click **Yes**.

#. Click **Yes** to synchronize the configuration.

#. Log in to the Master nodes as user **root**.

#. Run the **cd /opt/Bigdata/MRS_Current/*_*_ResourceManager/etc_UPDATED/** command to go to the **etc_UPDATED** directory.

#. Run the **grep '\\.queues' capacity-scheduler.xml -A2** command to display all configured queues and check whether the queues are consistent with those displayed on Manager.

   **root-default** is hidden on the Manager page.

   |image1|

#. .. _mrs_03_1163__li941013146411:

   Run the **grep '\\.capacity</name>' capacity-scheduler.xml -A2** command to display the value of each queue and check whether the value of each queue is the same as that displayed on Manager. Check whether the sum of the values configured for all queues is **100**.

   -  If the sum is **100**, the configuration is correct.
   -  If the sum is not **100**, the configuration is incorrect. Perform the following steps to rectify the fault.

#. Log in to MRS Manager, and select **Hosts**.

#. Determine the active Master node. The host name of the active Master node starts with a solid pentagon.

#. Log in to the active Master node as user **root**.

#. Run the **su - omm** command to switch to user **omm**.

#. Run the **sh /opt/Bigdata/om-0.0.1/sbin/restart-controller.sh** command to restart the controller when no operation is being performed on Manager.

   Restarting the controller will not affect the big data component services.

#. Repeat :ref:`1 <mrs_03_1163__li92876413199>` to :ref:`7 <mrs_03_1163__li941013146411>` to synchronize ResourceManager configurations and check whether the configurations are correct.

   If the latest configuration has not been loaded after the configuration synchronization is complete, a message will be displayed on the Manager page indicating that the configuration has expired. However, this will not affect services. The latest configuration will be automatically loaded when the component restarts.

.. |image1| image:: /_static/images/en-us_image_0000001392574346.png
