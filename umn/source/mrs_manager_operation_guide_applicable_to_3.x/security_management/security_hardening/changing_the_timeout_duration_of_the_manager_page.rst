:original_name: admin_guide_000410.html

.. _admin_guide_000410:

Changing the Timeout Duration of the Manager Page
=================================================

FusionInsight Manager allows you to configure the timeout duration of the Manager page based on service requirements. You must properly set the timeout duration to prevent information leakage in long-time exposure of the web page.

.. note::

   This function is supported only by MRS 3.3.0 or later.


Changing the Timeout Duration of the Manager Page
-------------------------------------------------

#. Log in to FusionInsight Manager.
#. Choose **System** > **OMS**.
#. In the list, locate the row that contains **tomcat** and click **Modify Configuration**.
#. On the displayed page, set **Session Timeout** as required and click **OK**.

   .. important::

      -  Set the minimum session duration based on service requirements. Otherwise, there will be security risks.
      -  Currently, you cannot use the method described as follows to change the timeout duration of component web UIs.
