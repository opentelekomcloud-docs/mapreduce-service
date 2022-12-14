:original_name: mrs_01_1183.html

.. _mrs_01_1183:

Using the Spark Client
======================

After an MRS cluster is created, you can create and submit jobs on the client. The client can be installed on nodes inside or outside the cluster.

-  Nodes inside the cluster: After an MRS cluster is created, the client has been installed on the master and core nodes in the cluster by default. For details, see `Using an MRS Client on Nodes Inside a Cluster <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0090.html>`__. Then, log in to the node where the MRS client is installed..
-  Nodes outside the cluster: You can install the client on nodes outside a cluster. For details about how to install a client, see `Using an MRS Client on Nodes Outside a Cluster <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0091.html>`__, and log in to the node where the MRS client is installed..


Using the Spark Client
----------------------

#. Based on the client location, log in to the node where the client is installed. For details, see `Using an MRS Client on Nodes Inside a Cluster <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0090.html>`__, or `Using an MRS Client on Nodes Outside a Cluster <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0091.html>`__.

#. Run the following command to go to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, run the following command to authenticate the user. In normal mode, user authentication is not required.

   **kinit** *Component service user*

#. Run the Spark shell command. The following provides an example:

   **spark-beeline**
