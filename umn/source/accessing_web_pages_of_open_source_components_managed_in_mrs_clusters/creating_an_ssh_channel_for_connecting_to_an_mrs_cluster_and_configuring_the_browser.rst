:original_name: mrs_01_0363.html

.. _mrs_01_0363:

Creating an SSH Channel for Connecting to an MRS Cluster and Configuring the Browser
====================================================================================

Scenario
--------

Users and an MRS cluster are in different networks. As a result, an SSH channel needs to be created to send users' requests for accessing websites to the MRS cluster and dynamically forward them to the target websites.

The MAC system does not support this function. For details about how to access MRS, see :ref:`EIP-based Access <mrs_01_0646>`.

Prerequisites
-------------

-  You have prepared an SSH client for creating the SSH channel, for example, the Git open-source SSH client. You have downloaded and installed the client.
-  You have created a cluster and prepared a key file in PEM format.
-  Users can access the Internet on the local PC.

Procedure
---------

#. Log in to the MRS management console and choose **Clusters** > **Active Clusters**.

#. Click the specified MRS cluster name.

   Record the security group of the cluster.

#. Add an inbound rule to the security group of the Master node to allow data access to the IP address of the MRS cluster through port **22**.

   For details, see **Virtual Private Cloud** > **User Guide** > **Security** > **Security Group** > **Adding a Security Group Rule**.

#. Query the primary management node of the cluster. For details, see :ref:`Determining Active and Standby Management Nodes of Manager <mrs_01_0086>`.

#. Bind an elastic IP address to the primary management node.

   For details, see **Virtual Private Cloud** > **User Guide** > **Elastic IP** > **Assigning an EIP and Binding It to an ECS**.

#. Start Git Bash locally and run the following command to log in to the active management node of the cluster: **ssh root@\ Elastic IP address** or **ssh -i** **Path of the key file** **root@**\ **Elastic IP address**.

#. Run the following command to view data forwarding configurations:

   **cat /etc/sysctl.conf \| grep net.ipv4.ip_forward**

   -  If **net.ipv4.ip_forward=1** is displayed, the forwarding function has been configured. Go to :ref:`9 <mrs_01_0363__l443dc566475c459399c4e15787485276>`.

   -  If **net.ipv4.ip_forward=0** is displayed, the forwarding function has not been configured. Go to :ref:`8 <mrs_01_0363__l116ba5c37fe940bc8218c6e3989bfa2a>`.

   -  If **net.ipv4.ip_forward** fails to be queried, this parameter has not been configured. Run the following command and then go to :ref:`9 <mrs_01_0363__l443dc566475c459399c4e15787485276>`:

      echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf

#. .. _mrs_01_0363__l116ba5c37fe940bc8218c6e3989bfa2a:

   Modify forwarding configurations on the node.

   a. Run the following command to switch to user **root**:

      **sudo su - root**

   b. Run the following commands to modify forwarding configurations:

      **echo 1 > /proc/sys/net/ipv4/ip_forward**

      **sed -i "s/net.ipv4.ip_forward=0/net.ipv4.ip_forward = 1/g" /etc/sysctl.conf**

      **sysctl -w net.ipv4.ip_forward=1**

   c. Run the following command to modify the **sshd** configuration file:

      **vi /etc/ssh/sshd_config**

      Press **I** to enter the edit mode. Locate **AllowTcpForwarding** and **GatewayPorts** and delete comment tags. Modify them as follows. Save the changes and exit.

      .. code-block::

         AllowTcpForwarding yes
         GatewayPorts yes

   d. Run the following command to restart the sshd service:

      **service sshd restart**

#. .. _mrs_01_0363__l443dc566475c459399c4e15787485276:

   Run the following command to view the floating IP address:

   **ifconfig**

   In the command output, **eth0:FI_HUE** indicates the floating IP address of Hue and **eth0:wsom** specifies the floating IP address of Manager. Record the value of **inet**.

   Run the **exit** command to exit.

#. .. _mrs_01_0363__lcf3e5d4b24e645bdbb9a0100a0dca09d:

   Run the following command on the local PC to create an SSH channel supporting dynamic port forwarding:

   **ssh -i** **Path of the key file -v -ND** **Local port** **root@\ Elastic IP address** or **ssh -v -ND Local port root@Elastic IP address**. After running the command, enter the password you set when you create the cluster.

   In the command, set **Local port** to the user's local port that is not occupied. Port **8157** is recommended.

   After the SSH channel is created, add **-D** to the command and run the command to start the dynamic port forwarding function. By default, the dynamic port forwarding function enables a SOCKS proxy process and monitors the user's local port. Port data will be forwarded to the primary management node using the SSH channel.

#. Run the following command to configure the browser proxy.

   a. Go to the Google Chrome client installation directory on the local PC.

   b. .. _mrs_01_0363__l2d621fbf73a04b28a135923e3a74a4f3:

      Press **Shift** and right-click the blank area, choose **Open Command Window Here** and enter the following command:

      **chrome --proxy-server="socks5://localhost:8157" --host-resolver-rules="MAP \* 0.0.0.0 , EXCLUDE localhost" --user-data-dir=c:/tmppath --proxy-bypass-list="*google*com,*gstatic.com,*gvt*.com,*:80"**

      .. note::

         -  In the preceding command, **8157** is the local proxy port configured in :ref:`10 <mrs_01_0363__lcf3e5d4b24e645bdbb9a0100a0dca09d>`.
         -  If the local OS is Windows 10, start the Windows OS, click **Start** and enter **cmd**. In the displayed CLI, run the command in :ref:`11.b <mrs_01_0363__l2d621fbf73a04b28a135923e3a74a4f3>`. If this method fails, click **Start**, enter the command in the search box, and run the command in :ref:`11.b <mrs_01_0363__l2d621fbf73a04b28a135923e3a74a4f3>`.

#. In the address box of the browser, enter the address for accessing Manager.

   Address format: **https://**\ *Floating IP address of MRS Manager*\ **:28443/web**

   The username and password of the MRS cluster need to be entered for accessing clusters with Kerberos authentication enabled, for example, user **admin**. They are not required for accessing clusters with Kerberos authentication disabled.

   When accessing Manager for the first time, you must add the address to the trusted site list.

#. Prepare the website access address.

   a. Obtain the website address format and the role instance according to :ref:`Web UIs <mrs_01_0362__sd893f53bb0b2400a8fe79f43dd2b7cf8>`.
   b. Click **Services**.
   c. Click the specified service name, for example, HDFS.
   d. Click **Instance** and view **Service IP Address** of **NameNode(Active)**.

#. In the address bar of the browser, enter the website address to access it.

#. When logging out of the website, terminate and close the SSH tunnel.
