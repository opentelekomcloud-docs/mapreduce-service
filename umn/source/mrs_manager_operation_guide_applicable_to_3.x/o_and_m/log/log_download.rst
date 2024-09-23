:original_name: admin_guide_000075.html

.. _admin_guide_000075:

Log Download
============

Scenario
--------

MRS Manager allows you to batch export logs generated on all instances of each service.

Procedure
---------

#. Log in to MRS Manager.

#. Choose **O&M** > **Log** > **Download**.

#. Select a log download range:

   a. **Service**: Click |image1| and select a service.
   b. **Host**: Enter the IP address of the host where the service is deployed. You can also click |image2| to select the required host.
   c. **Max. Concurrent Nodes**: Set the maximum number of concurrent nodes for log collection as you need. MRS 3.3.0 or later supports this parameter.
   d. Click |image3| in the upper right corner and configure **Start Time** and **End Time**.

#. Click **Download**.

   The downloaded log package contains the topology information of the start time and end time, helping you quickly find the log you need.

   The topology file is named in the format of **topo_<**\ *Topology structure change time*\ **>.txt**. The file contains the node IP address, host name, and service instances that reside on the node. (OMS nodes are identified by **Manager:Manager**.)

   Example:

   .. code-block::

      192.168.204.124|suse-124|DBService:DBServer;KrbClient:KerberosClient;LdapClient:SlapdClient;LdapServer:SlapdServer;Manager:Manager;meta:meta

.. |image1| image:: /_static/images/en-us_image_0000001392254938.png
.. |image2| image:: /_static/images/en-us_image_0000001392414466.png
.. |image3| image:: /_static/images/en-us_image_0000001392574062.png
