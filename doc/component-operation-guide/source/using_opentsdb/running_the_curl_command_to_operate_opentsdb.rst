:original_name: mrs_01_0472.html

.. _mrs_01_0472:

Running the curl Command to Operate OpenTSDB
============================================

Writing Data
------------

For example, to write data of a metric named **testdata**, whose timestamp is **1524900185**, value is **true**, tag is **key** and **value**, run the following command:

.. code-block:: text

   curl -ki -X POST -d '{"metric":"testdata", "timestamp":1524900185, "value":"true", "tags":{"key":"value"}}' https://<tsd_ip>:4242/api/put?sync

**<tsd_ip>**: indicates the IP address of the TSD instance of OpenTSDB to which data is to be written.

.. code-block::

   HTTP/1.1 204 No Content
   Content-Type: application/json; charset=UTF-8
   Content-Length:0

Querying Data
-------------

For example, to query summary information about the **testdata** metric in the past three years, run the following command:

.. code-block:: text

   curl -ks https://<tsd_ip>:4242/api/query?start=3y-ago\&m=sum:testdata | python -m json.tool

-  **<tsd_ip>**: indicates the IP address or host name of the TSD instance of OpenTSDB that needs to be accessed.
-  **<start=3y-ago\\&m=sum:testdata>**: Translates the **&** symbol, which may not be identified in the request.
-  (Optional) **<python -m json.tool>**: Converts the response request to the JSON format.

.. code-block::

   [
       {
           "aggregateTags": [],
           "dps": {
               "1524900185": 1
           },
           "metric": "testdata",
           "tags": {
               "key": "value"
           }
       }
   ]

Querying **tsd** Status
-----------------------

For example, to query information about the client connected to HBase, run the following command:

.. code-block:: text

   curl -ks https://<tsd_ip>:4242/api/stats/region_clients | python -m json.tool

**<tsd_ip>**: indicates the IP address of the TSD instance of OpenTSDB that needs to be accessed.

.. code-block::

   [
       {
           "dead": false,
           "endpoint":"/xx.xx.xx.xx:16020",
           "inflightBreached": 0,
           "pendingBatchedRPCs": 0,
           "pendingBreached": 0,
           "pendingRPCs": 0,
           "rpcResponsesTimedout": 0,
           "rpcResponsesUnknown": 0,
           "rpcid": 78,
           "rpcsInFlight": 0,
           "rpcsSent": 79,
           "rpcsTimedout": 0,
           "writesBlocked": 0
       }
   ]
