Lab 5.1 - Enable iControl LX extension management via GUI
---------------------------------------------------------

iControl LX extensions are distributed as RPMs (RedHat Package Management
system). In this lesson we will enable management of RPMs using the GUI. 


Task 1 - View iControl LX management is NOT available via the GUI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

iControl LX extensions can be installed on either the BIG-IP or iWorkflow
platforms. For this lab, we will use BIG-IP.

Perform the following steps to complete this task:

#. In your web browser, navigate to BIG-IP: ``https://10.1.1.245/``


#. Navigate to Main > iApps

   * You'll notice that iControl LX extension management is not available.

   .. image:: ../../_static/class1/module5/lab1-image001.png
      :align: center
      :scale: 50%


Task 2 - SSH to BIG-IP to enable iControl LX management via the GUI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform the following steps to complete this task:

#. Find and open the application ``PuTTY`` on the desktop, using the saved session 
   SSH to the BIG-IP_A.

#. At the bash shell enter the following command:

   ``touch /var/config/rest/iapps/enable``

#. Once the above command is issued, the BIG-IP can now manage iControl LX Extensions via the GUI.


Task 3 - View iControl LX management is now available via the GUI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform the following steps to complete this task:

#. In your web browser, navigate to BIG-IP: ``https://10.1.1.245/``. If it is already open, refresh the page.

#. Navigate to Main > iApps

   * You'll notice that iControl LX Extension management is now available.

   .. image:: ../../_static/class1/module5/lab1-image002.png
      :align: center
      :scale: 50%





