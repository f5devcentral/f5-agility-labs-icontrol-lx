Module 4 - Installing the HelloWorld extension
===============================================

In Module 4, we are going to create our first iControl LX Extension, the
``HelloWorld`` extension. It is a simple example that is perfect for
illustrating the package management system.

.. NOTE::

  In this lab we will be performing edits on the BIG-IP directly.
  This is not necessarily
  a best practice. You could also have a local version on your JumpHost and use
  ``Notepad++`` (already installed on your JumpHost, feel free to install
  something else) to do the work. Once your file is updated accordingly,
  you may use WinSCP to push the new version.

**Exercises in this Module**

- Lab 4.1 - Creating the Hello-World iControl LX Extension

  - Task 1 - Create our iControl LX Extension on BIG-IP
  - Task 2 - Check our iControl LX Extension is Working

- Lab 4.2 - Update our iControl LX Extension

  - Task 1 - Update our iControl LX Extension - Handle POST Requests
  - Task 2 - Update our iControl LX Extension - Perform a REST API Call

- Lab 4.3 - Create a new iControl LX RPM

  - Task 1 - Create a new RPM for the Updated iControl LX Extension
  - Task 2 - Retrieving your iControl LX Package

- Lab 4.4 - Install our iControl LX RPM

  - Task 1 - Review the Installed iControl LX Packages
  - Task 2 - Install our RPM
  - Task 3 - Test our iControl Extension

- Lab 4.5 - Delete the iControl LX Extension

  - Task 1 - Verify the 'packageName'
  - Task 2 - Create the 'delete' task
  - Task 3 - [OPTIONAL] Verify the iControl LX Extension was Deleted

.. toctree::
   :maxdepth: 1
   :glob:

   lab*
