:original_name: mrs_01_1786.html

.. _mrs_01_1786:

How to Resolve the Problem that Failed to Save Data When Using Internet Explorer 10 or Internet Explorer 11 ?
=============================================================================================================

Question
--------

Internet Explorer 11 or Internet Explorer 10 is used to access the web UI of Loader. After data is submitted, an error occurs.

Answer
------

-  Symptom

   #. When the submitted data is saved, a similar error occurs.

      |image1|

-  Causse

   Some Internet Explorer 11 versions convert POST requests into GET requests after receiving the HTTP 307 response. As a result, POST data cannot be delivered to the server.

-  Solution

   Use Google Chrome.

.. |image1| image:: /_static/images/en-us_image_0000001349139841.jpg
