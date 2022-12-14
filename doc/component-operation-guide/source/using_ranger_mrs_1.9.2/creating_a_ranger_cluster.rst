:original_name: mrs_01_0763.html

.. _mrs_01_0763:

Creating a Ranger Cluster
=========================

#. Create a cluster by referring to `Custom Creation of a Cluster <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0513.html>`__. Select the Ranger component during cluster creation.

   Currently, only normal MRS 1.9.2 clusters support Ranger. Security clusters with Kerberos authentication enabled do not support Ranger.

#. Configure other parameters by referring to `Custom Creation of a Cluster <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0513.html>`__.

   .. note::

      -  After the cluster is created, Ranger does not control users' permissions to access Hive and HBase.
      -  When Ranger is used to manage component permissions, for example, manage Hive table permissions, if a user submits a Hive job (operation on Hive data tables) on the interface or client, a message may be displayed indicating that the user does not have the permissions. In this case, you need to configure the database or table permissions for the user who submits the job in Ranger. For details, see the step for adding a policy in :ref:`Configuring Hive/Impala Access Permissions in Ranger <mrs_01_0765>` or :ref:`Configuring HBase Access Permissions in Ranger <mrs_01_0766>`.
