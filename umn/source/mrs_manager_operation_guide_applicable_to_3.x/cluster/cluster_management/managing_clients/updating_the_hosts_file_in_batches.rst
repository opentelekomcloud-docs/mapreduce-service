:original_name: admin_guide_000024.html

.. _admin_guide_000024:

Updating the hosts File in Batches
==================================

Scenario
--------

The client package downloaded from MRS Manager contains the client batch upgrade tool. This tool provides the function of upgrading clients in batches and the lightweight function of batch updating the **/etc/hosts** file on the node where the client is located.

Prerequisites
-------------

You have made preparations for the upgrade. For details, see "Prepare for the client upgrade." in :ref:`Batch Upgrading Clients <admin_guide_000023>`.


Updating the hosts File in Batches
----------------------------------

#. Check whether the user configured for the node where the **/etc/hosts** file needs to be updated is **root**.

   -  If yes, go to :ref:`2 <admin_guide_000024__li11411382418>`.
   -  If no, change the user to **root** and go to :ref:`2 <admin_guide_000024__li11411382418>`.

#. .. _admin_guide_000024__li11411382418:

   Run the **sh client_batch_upgrade.sh -r -f /tmp/FusionInsight-Client/FusionInsight_Cluster_1_Services_Client.tar -g /tmp/FusionInsight-Client/FusionInsight_Cluster_1_Services_ClientConfig/batch_upgrade/client-info.cfg** command to batch update the **/etc/hosts** file on the nodes where the client resides.

   .. note::

      -  When you batch update the **/etc/hosts** file, the entered client package can be a complete client package or a client package that contains only configuration files (recommended).
      -  The user configured for the host where the **/etc/hosts** file needs to be updated must be **root**. Otherwise, the update fails.
