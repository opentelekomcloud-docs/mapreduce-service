:original_name: mrs_02_0010.html

.. _mrs_02_0010:

Response
========

Status Code
-----------

After sending a request, you will receive a response, including a status code, response header, and response body.

A status code is a group of digits, ranging from 1\ *xx* to 5\ *xx*. It indicates the status of a request. For more information, see :ref:`Status Codes <mrs_02_0015>`.

For the API to `obtain request authentication <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__, if the status code **201** is returned after the API is called, the request is successful.

Response Header
---------------

Similar to a request, a response also has a header, for example, **Content-Type**.

:ref:`Figure 1 <mrs_02_0010__en-us_topic_0170155703_fig4865141011511>` shows the response header fields for the API used to `obtain request authentication <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__. The **x-subject-token** header field is the desired user token. This token can then be used to authenticate the calling of other APIs.

.. _mrs_02_0010__en-us_topic_0170155703_fig4865141011511:

.. figure:: /_static/images/en-us_image_0000001298246380.png
   :alt: **Figure 1** Header fields of the response to the request for obtaining a user token

   **Figure 1** Header fields of the response to the request for obtaining a user token

(Optional) Response Body
------------------------

This part is optional. The body of a response is often returned in structured format (for example, JSON or XML) as specified in the **Content-Type** header field. The response body transfers content except the response header.

The following shows the response body for the API to `obtain request authentication <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__. For the sake of space, only part of the content is displayed here.

.. code-block::

   {
       "token": {
           "expires_at": "2019-02-13T06:52:13.855000Z",
           "methods": [
               "password"
           ],
           "catalog": [
               {
                   "endpoints": [
                       {
           "region_id": "aaa"//The region ID "aaa" is used as an example.
   ...

If an error occurs during API calling, an error code and a message will be displayed. The following shows an error response body.

.. code-block::

   {
       "error_msg": "Invalid cluster name.",
       "error_code": "12000002"
   }

In the response body, **error_code** is an error code, and **error_msg** provides information about the error.
