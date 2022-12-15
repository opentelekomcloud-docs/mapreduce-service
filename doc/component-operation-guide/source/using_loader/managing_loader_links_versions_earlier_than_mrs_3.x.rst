:original_name: mrs_01_0403.html

.. _mrs_01_0403:

Managing Loader Links (Versions Earlier Than MRS 3.x)
=====================================================

Scenario
--------

You can create, view, edit, and delete links on the Loader page.

This section applies to versions earlier than MRS 3.x.

Prerequisites
-------------

You have accessed the Loader page. For details, see :ref:`Loader Page <mrs_01_0401__s12f4baccf3914471bee631d0ca198278>`.

Creating a Link
---------------

#. On the Loader page, click **Manage links**.

#. Click **New link** and configure link parameters.

   For details about the parameters, see :ref:`Loader Link Configuration <mrs_01_0402>`.

#. Click **Save**.

   If link configurations, for example, IP address, port, and access user information, are incorrect, the link will fail to be verified and saved. In addition, VPC configurations may affect the network connectivity.

   .. note::

      You can click **Test** to immediately check whether the link is available.

Viewing a Link
--------------

#. On the Loader page, click **Manage links**.

   -  If Kerberos authentication is enabled for the cluster, all links created by the current user are displayed by default and other users' links cannot be displayed.
   -  If Kerberos authentication is disabled for the cluster, all Loader links of the cluster are displayed.

#. In **Sqoop Links**, enter a link name to filter the link.

Editing a Link
--------------

#. On the Loader page, click **Manage links**.

#. Click the link name to go to the edit page.

#. .. _mrs_01_0403__l5be12d652055488480d006943dab4edb:

   Modify the link configuration parameters based on service requirements.

#. Click **Test**.

   If the test is successful, go to :ref:`5 <mrs_01_0403__l4e4fbb8553194cc8914e87c2ddde2152>`. If a message displays indicating that OBS server cannot be connected, repeat :ref:`3 <mrs_01_0403__l5be12d652055488480d006943dab4edb>`.

#. .. _mrs_01_0403__l4e4fbb8553194cc8914e87c2ddde2152:

   Click **Save**.

   If a Loader job has integrated into a Loader link, editing the link parameters may affect Loader running.

Deleting a Link
---------------

#. On the Loader page, click **Manage links**.

#. Locate the row that contains the target link, and click **Delete**.

#. In the dialog box, click **Yes, delete it**.

   If a Loader job has integrated a Loader link, the link cannot be deleted.
