:original_name: mrs_02_0011.html

.. _mrs_02_0011:

Obtaining a Project ID
======================

Obtaining a Project ID from the Management Console
--------------------------------------------------

A project ID (**project_id**) is required for some URLs when an API is called. To obtain a project ID, perform the following operations:

#. Log in to the management console.

#. Click the username and choose **My Credentials** from the drop-down list.

   On the **My Credentials** page, view project IDs in the project list.

If there are multiple projects in one region, expand **Region** and view subproject IDs in the **Project ID** column.

Obtaining a Project ID by Calling an API
----------------------------------------

You can obtain the project ID by calling the IAM API used to query project information based on the specified criteria.

The API used to obtain a project ID is **GET https://**\ *{Endpoint}*\ **/v3/projects**. *{Endpoint}* is the IAM endpoint and can be obtained from `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__. For details about API authentication, see :ref:`Authentication <mrs_02_0009>`.

The following is an example response. The value of **id** under **projects** is the project ID of the region specified by **name**.

.. code-block::

   {
       "projects": [
           {
               "domain_id": "65382450e8f64ac0870cd180d14e684b",
               "is_domain": false,
               "parent_id": "65382450e8f64ac0870cd180d14e684b",
               "name": "region_id",
               "description": "",
               "links": {
                   "next": null,
                   "previous": null,
                   "self": "https://www.example.com/v3/projects/a4a5d4098fb4474fa22cd05f897d6b99"
               },
               "id": "a4a5d4098fb4474fa22cd05f897d6b99",
               "enabled": true
           }
       ],
       "links": {
           "next": null,
           "previous": null,
           "self": "https://www.example.com/v3/projects"
       }
   }
