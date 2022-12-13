:original_name: mrs_01_1045.html

.. _mrs_01_1045:

Using Storm from Scratch
========================

You can submit and delete Storm topologies on the MRS cluster client.

Prerequisites
-------------

The MRS cluster client has been installed, for example, in the **/opt/hadoopclient** directory. The client directory in the following operations is only an example. Change it based on the actual installation directory onsite.

Procedure
---------

#. Prepare the client based on service requirements. Log in to the node where the client is installed.

#. Run the following command to switch to the client directory, for example, **/opt/hadoopclient**:

   **cd /opt/hadoopclient**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. For clusters with Kerberos authentication enabled, run the following command to authenticate the user. For clusters with Kerberos authentication disabled, skip this step.

   **kinit** *Storm user*

#. Run the following command to submit the Storm topology:

   **storm jar** *Path of the topology package Class name of the topology Main method Topology name*

   If the following information is displayed, the topology is submitted successfully.

   .. code-block::

      Finished submitting topology: topo1

#. Run the following command to query Storm topologies. For clusters with Kerberos authentication enabled, only users in the **stormadmin** or **storm** group can query all topologies.

   **storm list**

#. Run the following command to delete a Storm topology.

   **storm kill** *Topology name*
