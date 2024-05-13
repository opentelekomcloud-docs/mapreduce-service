:original_name: mrs_01_0645.html

.. _mrs_01_0645:

Access Through Direct Connect
=============================

MRS allows you to access MRS clusters using Direct Connect. Direct Connect is a high-speed, low-latency, stable, and secure dedicated network connection that connects your local data center to an online cloud VPC. It extends online cloud services and existing IT facilities to build a flexible, scalable hybrid cloud computing environment.

Prerequisites
-------------

Direct Connect is available, and the connection between the local data center and the online VPC has been established.

Accessing an MRS Cluster Using Direct Connect
---------------------------------------------

#. Log in to the MRS console.

#. Click the name of the cluster to enter its details page.

#. On the **Dashboard** tab page of the cluster details page, click **Access Manager** next to **MRS Manager**.

#. Set **Access Mode** to **Direct Connect** and select **I confirm that the network between the local PC and the floating IP address is connected and that MRS Manager is accessible using the Direct Connect connection**.

   The floating IP address is automatically allocated by MRS to access MRS Manager. Before using Direct Connect to access MRS Manager, ensure that the connection between the local data center and the online VPC has been established.

#. Click **OK**. The MRS Manager login page is displayed. Enter the username **admin** and the password set during cluster creation.

Switching the MRS Manager Access Mode
-------------------------------------

To facilitate user operations, the browser cache records the selected Manager access mode. To change the access mode, perform the following steps:

#. Log in to the MRS console.
#. Click the name of the cluster to enter its details page.
#. On the **Dashboard** tab page of the cluster details page, click |image1| next to **MRS Manager**.
#. On the displayed page, set **Access Mode**.

   -  To change **EIP** to **Direct Connect**, ensure that the network for direct connections is available, set **Access Mode** to **Direct Connect**, and select **I confirm that the network between the local PC and the floating IP address is connected and that MRS Manager is accessible using the Direct Connect connection**. Click **OK**.
   -  To change **Direct Connect** to **EIP**, set **Access Mode** to **EIP** and configure the EIP by referring to :ref:`Accessing MRS Manager Using an EIP <mrs_01_0102__en-us_topic_0035209594_section1511920110246>`. If a public IP address has been configured for the cluster, click **OK** to access MRS Manager using an EIP.

.. |image1| image:: /_static/images/en-us_image_0000001295738236.png
