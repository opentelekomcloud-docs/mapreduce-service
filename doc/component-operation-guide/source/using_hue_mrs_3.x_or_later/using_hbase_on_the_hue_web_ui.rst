:original_name: mrs_01_2371.html

.. _mrs_01_2371:

Using HBase on the Hue Web UI
=============================

Scenario
--------

You can use Hue to create or query HBase tables in a cluster and run tasks on the Hue web UI.

Make sure that the HBase component has been installed in the MRS cluster and the Thrift1Server instance has been added before this operation.

Accessing Job Browser
---------------------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.
#. Click HBase |image1|. The **HBase Browser** page is displayed.

Creating an HBase Table
-----------------------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.
#. Click HBase |image2|. The **HBase Browser** page is displayed.
#. Click **New Table** on the right, enter the table name and column family parameters, and click **Submit**.

Querying Data in an HBase Table
-------------------------------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.
#. Click HBase |image3|. The **HBase Browser** page is displayed.
#. Click the HBase table to be queried. Then, click the key value next to search box in the upper part, and query the HBase table.

.. |image1| image:: /_static/images/en-us_image_0000001295930632.png
.. |image2| image:: /_static/images/en-us_image_0000001296250104.png
.. |image3| image:: /_static/images/en-us_image_0000001349289781.png
