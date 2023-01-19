:original_name: mrs_01_1845.html

.. _mrs_01_1845:

How Do I Resolve the Problem that the Oozie Client Fails to Submit a MapReduce Job?
===================================================================================

Question
--------

The Oozie client fails to submit a MapReduce job and a message "Error: AUTHENTICATION: Could not authenticate, Authentication failed, status: 403, message: Forbidden" is displayed. How do I resolve this problem?

Answer
------

If the SolrServer or SolrServerAdmin instance is deployed on the node where the Oozie service is deployed, the Oozie client needs to use the host name of the node where the Oozie service locates to submit a job, but cannot use the service plane IP address of the node where the Oozie service locates.

For example, if the Oozie service is deployed on the host **hostname**, you need to run the **oozie job -oozie https://hostname:21003/oozie/ -config job.properties -run** command.
