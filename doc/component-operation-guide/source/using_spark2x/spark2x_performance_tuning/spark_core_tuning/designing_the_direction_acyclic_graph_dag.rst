:original_name: mrs_01_1983.html

.. _mrs_01_1983:

Designing the Direction Acyclic Graph (DAG)
===========================================

Scenario
--------

Optimal program structure helps increase execution efficiency. During application programming, avoid shuffle operations and combine narrow-dependency operations.

Procedure
---------

This topic describes how to design the DAG using the following example:

-  **Data format**: Time when a vehicle passes a toll station, license plate number, toll station number, and more
-  **Logic**: Two vehicles are determined to be traveling together if the following conditions are met:

   -  Both vehicles pass the same toll stations in the same sequence.
   -  The difference between the time that the vehicles pass the same toll station is smaller than a specified value.

There are two implementation ways for this example. :ref:`Figure 1 <mrs_01_1983__f20e2f35bb3d74f7ba062fffcc54f51bc>` shows the logic of implementation 1 and :ref:`Figure 2 <mrs_01_1983__f1f6a59d3ec254ae7bd46d3ace67fa3a7>` shows logic of implementation 2.

.. _mrs_01_1983__f20e2f35bb3d74f7ba062fffcc54f51bc:

.. figure:: /_static/images/en-us_image_0000001296250248.png
   :alt: **Figure 1** Implementation logic 1

   **Figure 1** Implementation logic 1

Logic description:

#. Collect information about the toll stations passed by each vehicle based on the vehicle license plate number and sort the toll stations.

   The following data is obtained: vehicle license plate number 1, [(time, toll station 3), (time, toll station 2), (time, toll station 4), (time, toll station 5)]

#. Determine the sequence in which the vehicle passed through.

   (toll station 3, (vehicle license plate number 1, time, 1st toll station))

   (toll station 2, (vehicle license plate number 1, time, 2nd toll station))

   (toll station 4, (vehicle license plate number 1, time, 3rd toll station))

   (toll station 5, (vehicle license plate number 1, time, 4th toll station))

#. Aggregate data by toll station.

   toll station 1, [(vehicle license plate number 1, time, 1st toll station), (vehicle license plate number 2, time, 5th toll station), (vehicle license plate number 3, time, 2nd toll station)]

#. Determine whether the time difference that two vehicles passed through the same toll station is below the specified value. If yes, fetch information about the two vehicles.

   (vehicle license plate number 1, vehicle license plate number 2),(1st toll station, 5th toll station)

   (vehicle license plate number 1, vehicle license plate number 3),(1st toll station, 2nd toll station)

#. Aggregate data based on the vehicle license plate numbers that passed through the same toll stations.

   (vehicle license plate number 1, vehicle license plate number 2), [(1st toll station, 5th toll station), (2nd toll station, 6th toll station), (1st toll station, 7th toll station), (3rd toll station, 8th toll station)]

#. If the two vehicles pass through the same toll stations in sequence, for example, toll stations 3, 4, 5 are the first, second, and third toll station passed by vehicle 1 and the 6th, 7th, and 8th toll station passed by vehicle 2, and the number of toll stations meets the specified requirements, the two vehicles are determined to be traveling together.

The logic of implementation 1 has the following disadvantages:

-  The logic is complex.
-  Too many shuffle operations affect performance.

.. _mrs_01_1983__f1f6a59d3ec254ae7bd46d3ace67fa3a7:

.. figure:: /_static/images/en-us_image_0000001349090445.png
   :alt: **Figure 2** Implementation logic 2

   **Figure 2** Implementation logic 2

Logic description:

#. Collect information about the toll stations passed by each vehicle based on the vehicle license plate number and sort the toll stations.

   The following data is obtained: vehicle license plate number 1, [(time, toll station 3), (time, toll station 2), (time, toll station 4), (time, toll station 5)]

#. Based on the number of toll stations (the number is 3 in this example) that must be passed by these vehicles, divide the toll station sequence as follows:

   toll station 3 > toll station 2 > toll station 4, (vehicle license plate number 1, [time passing through toll station 3, time passing through toll station 2, time passing through toll station 4])

   toll station 2 > toll station 4 > toll station 5, (vehicle license plate number 1, [time passing through toll station 2, time passing through toll station 4, time passing through toll station 5])

#. Aggregate information about vehicles that pass the same toll stations in the same sequence.

   toll station 3 > toll station 2 > toll station 4, [(vehicle license plate number 1, [time passing through toll station 3, time passing through toll station 2, time passing through toll station 4]), (vehicle license plate number 2, [time passing through toll station 3, time passing through toll station 2, time passing through toll station 4]), (vehicle license plate number 3, [time passing through toll station 3, time passing through toll station 2, time passing through toll station 4])]

#. Determine whether the time difference that these vehicles passed through the same toll station is below the specified value. If yes, the vehicles are determined to be traveling together.

The logic of implementation 2 has the following advantages:

-  The logic is simplified.
-  One **groupByKey** is reduced, that is, one less shuffle operation is performed. It helps improve performance.
