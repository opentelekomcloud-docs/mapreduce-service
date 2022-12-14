:original_name: mrs_01_0864.html

.. _mrs_01_0864:

Configuring the Additional Scheduler WebUI
==========================================

Scenario
--------

If the custom scheduler is set in ResourceManager, you can set the corresponding web page and other Web applications for the custom scheduler.

Configuration Description
-------------------------

Go to the **All Configurations** page of Yarn and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

.. table:: **Table 1** Configuring the Additional Scheduler WebUI

   +---------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                                   | Description                                                                                                                                                                        | Default Value |
   +=============================================+====================================================================================================================================================================================+===============+
   | hadoop.http.rmwebapp.scheduler.page.classes | Load the corresponding web page for the custom scheduler on the RM WebUI. This parameter is valid only when **yarn.resourcemanager.scheduler.class** is set to a custom scheduler. | ``-``         |
   +---------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | yarn.http.rmwebapp.external.classes         | Load the custom web application in the RM Web service.                                                                                                                             | ``-``         |
   +---------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
