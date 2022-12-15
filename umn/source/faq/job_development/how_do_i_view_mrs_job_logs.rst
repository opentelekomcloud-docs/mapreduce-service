:original_name: mrs_03_1172.html

.. _mrs_03_1172:

How Do I View MRS Job Logs?
===========================

#. .. _mrs_03_1172__li943507288:

   On the **Jobs** page of the MRS console, you can view logs of each job, including launcherJob and realJob logs.

   -  Generally, error logs are printed in **stderr** and **stdout** for launcherJob jobs, as shown in the following figure:

      |image1|

   -  You can view realJob logs on the ResourceManager web UI provided by the Yarn service on MRS Manager.

      |image2|

#. Log in to the Master node of the cluster to obtain the job log files in :ref:`1 <mrs_03_1172__li943507288>`. The HDFS path is **/tmp/logs/**\ *{submit_user}*\ **/logs/**\ *{application_id}*.

#. After the job is submitted, if the job application ID cannot be found on the Yarn web UI, the job fails to be submitted. You can log in to the active Master node of the cluster and view the job submission process log **/var/log/executor/logs/exe.log**.

.. |image1| image:: /_static/images/en-us_image_0000001151963015.png
.. |image2| image:: /_static/images/en-us_image_0000001438033333.png
