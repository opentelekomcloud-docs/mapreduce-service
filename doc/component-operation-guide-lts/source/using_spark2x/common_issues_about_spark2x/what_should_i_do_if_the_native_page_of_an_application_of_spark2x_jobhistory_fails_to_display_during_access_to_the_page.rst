:original_name: mrs_01_2064.html

.. _mrs_01_2064:

What Should I Do If the Native Page of an Application of Spark2x JobHistory Fails to Display During Access to the Page
======================================================================================================================

Question
--------

After a Spark application that contains a job with millions of tasks. After the application creation is complete, if you access the native page of the application in JobHistory, the native page of the application can be displayed after a long time. If the native page cannot be displayed within 10 minutes, Error information will be generated for the Proxy.


.. figure:: /_static/images/en-us_image_0000001829035105.png
   :alt: **Figure 1** Error information example

   **Figure 1** Error information example

Answer
------

When you switch to the native page of an application on the JobHistory page, JobHistory needs to play back the event log of the application. If the application contains a large number of event logs, the playback takes a long time and the browser takes a long time to navigate you to the native page.

The current browser uses the HTTPd as the proxy to access the JobHistory native page. The proxy timeout duration is 10 minutes. Therefore, if the JobHistory cannot parse the event log and return the result within 10 minutes, the HTTPd automatically returns the proxy error information to the browser.

Solution
--------

The local disk cache function is enabled on the JobHistory. When a user accesses an application, the event log of the application is cached on the local disk. In this case, the response speed can be greatly accelerated for the second access. Therefore, in this case, you only need to wait for a while and then access the link again. For the second time, you do not need to wait for a long time.
