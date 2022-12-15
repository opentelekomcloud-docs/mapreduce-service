:original_name: mrs_08_0035.html

.. _mrs_08_0035:

OpenTSDB
========

OpenTSDB is a distributed, scalable time series database based on HBase. OpenTSDB is designed to collect monitoring information of a large-scale cluster and implement second-level data query, eliminating the limitations of querying and storing massive amounts of monitoring data in common databases.

OpenTSDB consists of a Time Series Daemon (TSD) as well as a set of command line utilities. Interaction with OpenTSDB is primarily implemented by running one or more TSDs. Each TSD is independent. There is no master server and no shared state, so you can run as many TSDs as required to handle any load you throw at it. Each TSD uses HBase in a CloudTable cluster to store and retrieve time series data. The data schema is highly optimized for fast aggregations of similar time series to minimize storage space. TSD users never need to directly access the underlying storage. You can communicate with the TSD through an HTTP API. All communications happen on the same port (the TSD figures out the protocol of the client by looking at the first few bytes it receives).


.. figure:: /_static/images/en-us_image_0000001296430758.png
   :alt: **Figure 1** OpenTSDB architecture

   **Figure 1** OpenTSDB architecture

Application scenarios of OpenTSDB have the following features:

-  The collected metrics have a unique value at a time point and do not have a complex structure or relationship.
-  Monitoring metrics change with time.
-  Like HBase, OpenTSDB features high throughput and good scalability.

OpenTSDB provides an HTTP based application programming interface to enable integration with external systems. Almost all OpenTSDB features are accessible via the API such as querying time series data, managing metadata, and storing data points. For details, visit https://opentsdb.net/docs/build/html/api_http/index.html.
