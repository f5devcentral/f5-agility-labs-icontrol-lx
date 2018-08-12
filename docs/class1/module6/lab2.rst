Lab 6.2 - Run playbook to create ASM policy and associate with virtual server
-----------------------------------------------------------------------------

In this lesson we will use Ansible to deploy a new ASM policy and attach that policy
to an existing virtual server. 


Task 1 - Run playbook from the Ubuntu host
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. On your Xubuntu Server you should be at a prompt that looks like this: 
   
   ``external_user@xubuntu-vm:~/f5-ansible$``
   
   You should be in the "f5-ansible" directory.


#. At the prompt type the following:
   
   ``ansible-playbook playbooks/ASM_create_apply.yml``

   Once you run the above command, you will see the playbook execute. You will see each task executing and the status of each task.  The last two lines will give
   you a summary of the playbook execution and will indicate if it was ok or failed. The 
   playbook will take up to 30 seconds to complete.  Also note you will see some ``DEPRECATION WARNING`` messages which can be ignored for this lab.

   .. Note:: If you wish to view the contents of the playbook you can use the following command:

      ``cat playbooks/ASM_create_apply.yml``

#. Now that we've run the playbook, let's look to see if an ASM policy has been created. It should have the name
   ``iControlLX_Agility2018_Ansible``. Navigate to Main > Security > Application Security >
   Security Policies to view the ASM policies.

   .. image:: ../../_static/class1/module6/lab2-image001.png
      :align: center
      :scale: 50%

#. Now let's look at the virtual server to see if the policy has been associated. Navigate
   to Main > Local Traffic > Virtual Server > Virtual Server List then select ``hackazon_virtual``.
   Once selected navigate to Security > Policies.

   .. image:: ../../_static/class1/module6/lab2-image002.png
      :align: center
      :scale: 50%

#. Congratulations! You've now created an ASM policy and associated it with a virtual server all in a single step!

.. NOTE:: You have reached the end of this lab. In this lab, you have learned about iControl LX Extensions, including how to create, install and use them. You have also learned how to create an ASM policy in a single REST call. Lastly, you have learned how to associate an ASM policy with a virtual server in a single command using an Ansible playbook. Great job! 

