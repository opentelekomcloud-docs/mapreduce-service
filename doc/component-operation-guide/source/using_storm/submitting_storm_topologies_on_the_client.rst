:original_name: mrs_01_0381.html

.. _mrs_01_0381:

Submitting Storm Topologies on the Client
=========================================

Scenario
--------

You can submit Storm topologies on the cluster client to continuously process stream data. For clusters with Kerberos authentication enabled, users who submit topologies must be members of the **stormadmin** or **storm** group.

Prerequisites
-------------

The client has been updated.

Procedure
---------

#. Prepare the client based on service requirements. Log in to the node where the client is installed.

#. Run the following command to set the permissions on the topology JAR file:

   For example, run the following command to change the permissions on **/opt/storm/topology.jar**:

   **chmod 600 /opt/storm/topology.jar**

#. Run the following command to switch to the client directory, for example, **/opt/client**.

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If multiple Storm instances are installed, run the following command to load the environment variables of a specific instance when running the Storm command to submit the topology. Otherwise, skip this step. The following command uses the instance Storm-2 as an example.

   **source Storm-2/component_env**

#. For clusters with Kerberos authentication enabled, run the following command to authenticate the user. For clusters with Kerberos authentication disabled, skip this step.

   **kinit** *Storm user*

#. For versions earlier than MRS 3.x, run the following command to submit the Storm topology:

   **storm jar** *Path of the topology package Class name of the topology Main method Topology name*

   If the following information is displayed, the topology is submitted successfully.

   .. code-block::

      Finished submitting topology: topo1

   .. note::

      -  To support sampling messages, add the **topology.debug** and **topology.eventlogger.executors** parameters.
      -  Data processing methods vary with topologies. The topology in the example generates characters randomly and separates character strings. To query the processing status, enable the sampling function and perform operations according to :ref:`Querying Storm Topology Logs <mrs_01_0384>`.

#. Run the following command to submit a topology task for MRS 3.x or later:

   **storm jar** *topology-jar-path* *class input parameter list*

   -  *topology-jar-path* indicates the path of the JAR file of the topology.
   -  *class* indicates the class name of the main method used by the topology.
   -  *Input parameter list* includes input parameters of the main method used by the topology.

   If the following information is displayed, the topology is submitted successfully:

   .. code-block::

      Finished submitting topology: topology1

   .. note::

      -  The login authentication user must correspond to the loaded environment variable (**component_env**). Otherwise, an error occurs when you run the **storm** command to submit the topology task.
      -  After the client environment variable is loaded and the corresponding user login succeeds, the user can run the Storm command on any Storm client to submit the topology task. After the command is executed, the successfully submitted topology is still in the Storm cluster of the user.
      -  If cluster domain name is modified, you need to reset the domain name before submitting the topology. Run the cql statement.

#. Run the following command to query Storm topologies. For clusters with Kerberos authentication enabled, only users in the **stormadmin** or **storm** group can query all topologies.

   **storm list**
