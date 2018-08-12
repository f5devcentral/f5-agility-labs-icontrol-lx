Lab 5.4 -  Creating an ASM Policy by calling the iControl LX extension
----------------------------------------------------------------------

In this lab we will use the Postman client to create an ASM policy in a single
call to the BIG-IP.


Task 1 - Check BIG-IP for existing ASM policies
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First let's take a look at the existing policies on the BIG-IP.

#. In your web browser, navigate to BIG-IP: ``https://10.1.1.245/``

#. Navigate to Main > Security > Application Security > Security Policies

   .. image:: ../../_static/class1/module5/lab4-image001.png
      :align: center
      :scale: 50%


#. As seen in the sceenshot above there are no existing policies on the BIG-IP.


Task 2 - Perform REST call using Postman to create policy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now let's use Postman to create an ASM policy.

First we have to authenticate to the BIG-IP and obtain a token using Postman. 

#. Select ``Step1: Request token from BIG-IP`` from the collections tab, then select ``Send``.

   .. image:: ../../_static/class1/module5/lab4-image002.png
      :align: center
      :scale: 50%

   .. NOTE:: In this and subsequent steps, please take a moment to review the content of each request in Postman. This will help familiarize you with REST API syntax, as well as how to interact with the REST API from a third-party client. 

#. This will generate a token used to authenticate future REST calls from Postman.

#. Select ``Step2: Increase Auth Token Timeout on BIG-IP`` from the collections tab, then select 
   ``Send``. This will extend the token timeout to 36000 seconds.

   .. image:: ../../_static/class1/module5/lab4-image003.png
      :align: center
      :scale: 50% 

#. Select ``iControl LX ASM Create Policy POST`` from the collections tab, then select ``Send``.
   This will create an ASM policy using the iControl LX RPM package uploaded earlier.  Note the 
   POST body contains only a name for the policy, in this case the name is "iControlLX_Agility2018".
   This will be the name of the ASM policy that's created on the BIG-IP. 

   .. image:: ../../_static/class1/module5/lab4-image004.png
      :align: center
      :scale: 50%

   .. NOTE:: It will take about 15-20 seconds to generate the policy after hitting the
      ``Send`` button in Postman. Please wait this amount of time before proceeding to the following
      task.

Task 3 - Verify ASM policy has been created
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

There are two different ways we will verify that the ASM policy has been created. We will check
using Postman and will also check via the GUI.

#. To check if the policy has been created using Postman, select ``iControl LX ASM Create Policy GET`` 
   from the collections tab, then select ``Send``. Look for the field ``id:<unique_id>`` in 
   the response. This will tell you the policy has been created.

   .. image:: ../../_static/class1/module5/lab4-image005.png
      :align: center
      :scale: 50%

#. To check if the policy has been created using the GUI, in your web browser  
   navigate to BIG-IP: ``https://10.1.1.245/``.  Then navigate to 
   Main > Security > Application Security > Security Policies.  You will see the newly created policy.

   .. image:: ../../_static/class1/module5/lab4-image006.png
      :align: center
      :scale: 50%

   .. NOTE:: What have we accomplished?  We used Postman to create an ASM policy by only sending the
      name of the policy. The iControl LX Extension that we installed on the BIG-IP, ``SecurityAdd-0.2-002.noarch.rpm``, 
      accepts the name of the policy then executes the rest of the requirements to build the policy. 
      The policy is now ready to be associated with a Virtual Server. 


