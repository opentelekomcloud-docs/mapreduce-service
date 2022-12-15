:original_name: mrs_01_0083.html

.. _mrs_01_0083:

Logging In to an ECS
====================

This section describes how to remotely log in to an ECS in an MRS cluster using the remote login (VNC mode) function provided on the ECS management console or a key or password (SSH mode). Remote login (VNC mode) is mainly used for emergency O&M. In other scenarios, it is recommended that you log in to the ECS using SSH.

.. note::

   To log in to a cluster node using SSH, you need to manually add an inbound rule in the security group of the cluster. The source address is **Client IPv4 address/32** (or **Client IPv6 address/128**) and the port number is **22**. For details, see **Virtual Private Cloud** > **User Guide** > ****Security > Security Group** > **Adding a Security Group Rule****.

Logging In to an ECS Using VNC
------------------------------

#. Log in to the MRS management console.
#. Click |image1| in the upper-left corner on the management console and select a region and project.
#. Choose **Clusters > Active Clusters**, select a running cluster, and click its name to switch to the cluster details page.
#. On the **Nodes** tab page, click the name of a Master node in the Master node group to log in to the ECS management console.
#. In the upper right corner, click **Remote Login**.
#. Perform subsequent operations by referring to `Login Using VNC <https://docs.otc.t-systems.com/en-us/usermanual/ecs/en-us_topic_0093263550.html>`__.

.. _mrs_01_0083__section5513107114:

Logging In to an ECS Using a Key Pair (SSH)
-------------------------------------------

**Logging In to the ECS from Local Windows**

To log in to the Linux ECS from local Windows, perform the operations described in this section. The following procedure uses PuTTY as an example to log in to the ECS.

#. Log in to the MRS management console.

#. Click |image2| in the upper-left corner on the management console and select a region and project.

#. Choose **Clusters** > **Active Clusters**, select a running cluster, and click its name to switch to the cluster details page.

#. On the **Nodes** tab page, click the name of a Master node in the Master node group to log in to the ECS management console.

#. Click the **EIPs** tab, click **Bind EIP** to bind an EIP to the ECS, and record the EIP. If an EIP has been bound to the ECS, skip this step.

#. Check whether the private key file has been converted to **.ppk** format.

   -  If yes, go to :ref:`11 <mrs_01_0083__li99981049191918>`.
   -  If no, go to :ref:`7 <mrs_01_0083__li1090865924810>`.

#. .. _mrs_01_0083__li1090865924810:

   Run PuTTY.

#. In the **Actions** area, click **Load** and import the private key file you used during ECS creation.

   Ensure that the private key file is in the format of **All files (*.*)**.

#. Click **Save private key**.

#. .. _mrs_01_0083__li499810490191:

   Save the converted private key, for example, **kp-123.ppk**, to a local directory.

#. .. _mrs_01_0083__li99981049191918:

   Run PuTTY.

#. Choose **Connection** > **Data**. Enter the image username in **Auto-login username**.

   .. note::

      The image username for cluster nodes is **root**.

#. Choose **Connection** > **SSH** > **Auth**. In the last configuration item **Private key file for authentication**, click **Browse** and select the private key converted in :ref:`10 <mrs_01_0083__li499810490191>`.

#. Click **Session**.

   a. **Host Name (or IP address)**: Enter the EIP bound to the ECS.

   b. **Port**: Enter **22**.

   c. **Connection Type**: Select **SSH**.

   d. **Saved Sessions**: Task name, which can be clicked for remote connection when you use PuTTY next time


      .. figure:: /_static/images/en-us_image_0000001295898104.png
         :alt: **Figure 1** Clicking **Session**

         **Figure 1** Clicking **Session**

#. Click **Open** to log in to the ECS.

   If you log in to the ECS for the first time, PuTTY displays a security warning dialog box, asking you whether to accept the ECS security certificate. Click **Yes** to save the certificate to your local registry.

**Logging In to the ECS from Local Linux**

To log in to the Linux ECS from local Linux, perform the operations described in this section. The following procedure uses private key file **kp-123.pem** as an example to log in to the ECS. The name of your private key file may differ.

#. On the Linux CLI, run the following command to change operation permissions:

   **chmod 400 /path/kp-123.pem**

   .. note::

      In the preceding command, *path* refers to the path where the key file is saved.

#. Run the following command to log in to the ECS:

   **ssh -i /path/kp-123.pem**\ *Default username*\ @\ *EIP*

   For example, if the default username is **root** and the EIP is **123.123.123.123**, run the following command:

   ssh -i /*path*/kp-123.pem root@123.123.123.123

   .. note::

      -  *path* indicates the path where the key file is saved.
      -  *EIP* indicates the EIP bound to the ECS.
      -  For cluster nodes of versions earlier than MRS 1.6.2, the image username is **Linux**.
      -  The image username is **root** for cluster nodes of MRS 1.6.2 or later.

Changing the OS Keyboard Language
---------------------------------

All nodes in the MRS cluster run the Linux OS. For details about how to change the OS keyboard language, see **Getting Started** > **Logging In to an ECS** > **Logging In to an ECS Using VNC** in the *Elastic Cloud Server User Guide*.

.. |image1| image:: /_static/images/en-us_image_0000001349257245.png
.. |image2| image:: /_static/images/en-us_image_0000001349137661.png
