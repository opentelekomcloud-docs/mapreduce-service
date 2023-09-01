:original_name: mrs_03_1214.html

.. _mrs_03_1214:

How Do I Do If Sessions Are Not Released After Hue Connects to HiveServer and the Error Message "over max user connections" Is Displayed?
=========================================================================================================================================

Applicable versions: MRS 3.1.0 and earlier

#. Modify the following file on the two Hue nodes:

   /opt/Bigdata/FusionInsight_Porter_8.*/install/FusionInsight-Hue-``*``/hue/apps/beeswax/src/beeswax/models.py

#. Change the configurations in lines 396 and 404.

   Change **q Changed = self.filter(owner=user, application=application).exclude(guid='').exclude(secret='')** to **q = self.filter(owner=user, application=application).exclude(guid=None).exclude(secret=None)**.

   |image1|

.. |image1| image:: /_static/images/en-us_image_0000001392255290.png
