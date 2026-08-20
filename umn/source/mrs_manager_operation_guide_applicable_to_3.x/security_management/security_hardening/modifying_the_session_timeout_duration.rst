:original_name: admin_guide_000410.html

.. _admin_guide_000410:

Modifying the Session Timeout Duration
======================================

MRS Manager allows you to configure the timeout duration of the Manager page and component Web UI page available in MRS 3.6.0 or later based on service requirements. You must properly set the timeout duration to prevent information leakage in long-time exposure of the web page.

.. note::

   This function is supported only by MRS 3.3.0 or later.

Modifying the Timeout Duration
------------------------------

#. Log in to MRS Manager.
#. Choose **System** > **OMS**.
#. In the list, locate the row that contains **tomcat** and click **Modify Configuration**.
#. On the displayed page, set **Session Timeout** as required and click **OK**.

   .. important::

      -  Set the minimum session duration based on service requirements. Otherwise, there will be security risks.
      -  To modify the timeout duration of the component Web UI, restart the instance with expired configuration after setting the session timeout duration. (Available in MRS 3.6.0 or later)
