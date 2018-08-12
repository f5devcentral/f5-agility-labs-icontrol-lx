Lab 5.3 - Setup Postman to interact with the iControl LX Extension
------------------------------------------------------------------

In this lab we will setup the Postman client to be able to interact
with the iControl LX Extension we installed in the previous step.

Task 1 - Setup Postman client
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use Postman
~~~~~~~~~~~

Perform the following steps to complete this task:

#. Open the Postman application on your Windows jumphost. An icon for Postman can be found on the Desktop. If you are prompted to update, click Remind me later. Click X to close the modal launch screen window. Select the environment labeled
   ``ASM_ENVIRONMENT`` in the upper-right hand side of Postman application if it is not already selected. 

   .. image:: ../../_static/class1/module5/lab3-image001.png
      :align: center
      :scale: 50%


#. If needed, on the left-hand column select Collections, then ``iControl LX Lab`` which
   will contain all the REST calls needed for this lab.

   .. image:: ../../_static/class1/module5/lab3-image002.png
      :align: center
      :scale: 50%


#. In the ``iControl LX Lab`` Collection you have four available items:

   * Authenticating to the BIG-IP and obtaining a token
   * Extending the timeout of the token
   * Creating an ASM policy using the iControl LX Extension
   * Checking for the policy ID of a recently created ASM policy using the iControl LX Extension


