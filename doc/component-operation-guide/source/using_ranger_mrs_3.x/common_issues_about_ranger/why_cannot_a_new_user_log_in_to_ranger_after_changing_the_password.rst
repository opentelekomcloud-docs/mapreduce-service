:original_name: mrs_01_2300.html

.. _mrs_01_2300:

Why Cannot a New User Log In to Ranger After Changing the Password?
===================================================================

Question
--------

When a new user logs in to Ranger, why is the 401 error reported after the password is changed?

Answer
------

The UserSync synchronizes user data at an interval of 5 minutes by default. Therefore, a new user created on Manager cannot log in to the Ranger before the user data is successfully synchronized because the Ranger database does not have the user information. The user can log in to the Ranger only after the specified interval ends.

In non-security mode, the Ranger does not synchronize user data from Manager. Therefore, only the **admin** user can log in to the Ranger page.
