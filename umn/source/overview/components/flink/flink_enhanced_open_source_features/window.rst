:original_name: mrs_08_00345.html

.. _mrs_08_00345:

Window
======

Enhanced Open Source Feature: Window
------------------------------------

This section describes the sliding window of Flink and provides the sliding window optimization method. For details about windows, visit https://ci.apache.org/projects/flink/flink-docs-release-1.12/dev/stream/operators/windows.html.

**Introduction to Window**

Data in a window is saved as intermediate results or original data. If you perform a sum operation (**window(SlidingEventTimeWindows.of(Time.seconds(20), Time.seconds(5))).sum**) on data in the window, only the intermediate result will be retained. If a custom window (**window(SlidingEventTimeWindows.of(Time.seconds(20), Time.seconds(5))).apply(new UDF)**) is used, all original data in the window will be saved.

If custom windows **SlidingEventTimeWindow** and **SlidingProcessingTimeWindow** are used, data is saved as multiple backups. Assume that the window is defined as follows:

.. code-block::

   window(SlidingEventTimeWindows.of(Time.seconds(20), Time.seconds(5))).apply(new UDFWindowFunction)

If a block of data arrives, it is assigned to four different windows (20/5 = 4). That is, the data is saved as four copies in the memory. When the window size or sliding period is set to a large value, data will be saved as excessive copies, causing redundancy.


.. figure:: /_static/images/en-us_image_0000001349390625.png
   :alt: **Figure 1** Original structure of a window

   **Figure 1** Original structure of a window

If a data block arrives at the 102nd second, it is assigned to windows [85, 105), [90, 110), [95, 115), and [100, 120).

**Window Optimization**

As mentioned in the preceding, there are excessive data copies when original data is saved in SlidingEventTimeWindow and SlidingProcessingTimeWindow. To resolve this problem, the window that stores the original data is restructured, which optimizes the storage and greatly lowers the storage space. The window optimization scheme is as follows:

#. Use the sliding period as a unit to divide a window into different panes.

   A window consists of one or multiple panes. A pane is essentially a sliding period. For example, the sliding period (namely, the pane) of **window(SlidingEventTimeWindows.of(Time.seconds(20), Time.seconds.of(5)))** lasts for 5 seconds. If this window ranges from [100, 120), this window can be divided into panes [100, 105), [105, 110), [110, 115), and [115, 120).


   .. figure:: /_static/images/en-us_image_0000001296430762.png
      :alt: **Figure 2** Window optimization

      **Figure 2** Window optimization

#. When a data block arrives, it is not assigned to a specific window. Instead, Flink determines the pane to which the data block belongs based on the timestamp of the data block, and saves the data block into the pane.

   A data block is saved only in one pane. In this case, only a data copy exists in the memory.


   .. figure:: /_static/images/en-us_image_0000001296590610.png
      :alt: **Figure 3** Saving data in a window

      **Figure 3** Saving data in a window

#. To trigger a window, compute all panes contained in the window, and combine all these panes into a complete window.


   .. figure:: /_static/images/en-us_image_0000001349110457.png
      :alt: **Figure 4** Triggering a window

      **Figure 4** Triggering a window

#. If a pane is not required, you can delete it from the memory.


   .. figure:: /_static/images/en-us_image_0000001349309913.png
      :alt: **Figure 5** Deleting a window

      **Figure 5** Deleting a window

After optimization, the quantity of data copies in the memory and snapshot is greatly reduced.
