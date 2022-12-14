:original_name: mrs_01_0959.html

.. _mrs_01_0959:

Access Control of a Dynamic Table View on Hive
==============================================

Scenario
--------

This section describes how to create a view on Hive when MRS is configured in security mode, authorize access permissions to different users, and specify that different users access different data.

In the view, Hive can obtain the built-in function **current_user()** of the users who submit tasks on the client and filter the users. This way, authorized users can only access specific data in the view.

.. note::

   In normal mode, the **current_user()** function cannot distinguish users who submit tasks on the client. Therefore, the access control function takes effect only for Hive in security mode.

   If the **current_user()** function is used in the actual service logic, the possible risks must be fully evaluated during the conversion between the security mode and normal mode.

Operation Example
-----------------

-  If the current_user function is not used, different views need to be created for different users to access different data.

   -  Authorize the view **v1** permission to user **hiveuser1**. The user **hiveuser1** can access data with **type** set to **hiveuser1** in **table1**.

      **create view v1 as select \* from table1 where type='hiveuser1'**

   -  Authorize the view **v2** permission to user **hiveuser2**. The user **hiveuser2** can access data with **type** set to **hiveuser2** in **table1**.

      **create view v2 as select \* from table1 where type='hiveuser2'**

-  If the current_user function is used, only one view needs to be created.

   Authorize the view **v** permission to users **hiveuser1** and **hiveuser2**. When user **hiveuser1** queries view **v**, the current_user() function is automatically converted to **hiveuser1**. When user **hiveuser2** queries view **v**, the **current_user()** function is automatically converted to **hiveuser2**.

   **create view v as select \* from table1 where type=current_user()**
