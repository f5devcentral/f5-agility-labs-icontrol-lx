Module 6 - Using Ansible to create an ASM policy and associate it with a Virtual Server
=======================================================================================

In module 6, we are going to use Ansible_ and Ansible playbooks to deploy a new ASM policy 
and attach the new policy to an existing virtual server. We will leverage the same iControl LX
extension to build the ASM policy except this time Ansible will be the client. Ansible also
has F5 modules that can be used to associate the newly created policy to a virtual server.

   .. _Ansible: https://www.ansible.com/integrations/networks/f5

Ansible F5 modules enable most common use cases, such as:

    * Automating the initial configurations on the BIG-IP like DNS, NTP etc.
    * Automation to network the BIG-IP (VLANS, Self-IPs)
    * Automated deployment of HTTP and HTTPS applications
    * Managing Virtual Servers, Pools, Monitors and other configuration objects

**Exercises in this Module**

- Lab 6.1 - Brief overview of our Ansible setup

  - Task 1 - Inventory, playbooks, ansible.cfg
  - Task 2 - View ASM policies and view there are no ASM policies associated with ``hackazon_virtual``
    virtual server. 

- Lab 6.2 - Run playbook to create ASM policy and associate with virtual server

  - Task 1 - Run the playbook ``ASM_create_apply`` to build policy and attach to virtual server
  - Task 2 - Verify new ASM policy was created and associated to virtual server

.. toctree::
   :maxdepth: 1
   :glob:

   lab*
