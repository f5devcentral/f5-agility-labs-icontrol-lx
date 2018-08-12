Lab 4.4 - Install our iControl LX RPM
-------------------------------------

Let's try to install our iControl LX RPM on BIG-IP.

To install the iControl LX Extension, you'll first need to copy the iControl LX
package onto your BIG-IP device into the correct folder. It should be in the
following directory: ``/var/config/rest/downloads``. 

Use your BIG-IP SSH session and run the following command:

``mv /var/config/rest/iapps/RPMS/HelloWorld-0.1-001.noarch.rpm /var/config/rest/downloads/``

Since the RPM package was already on the BIG-IP we just had to move it to the correct folder. You can verify the transfer was successful by checking the
folder ``/var/config/rest/downloads``.


Task 1 - Review the installed iControl LX Packages
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First let's take a look at the packages installed on the BIG-IP.

Perform the following steps to complete this task:

#. From your Xubuntu Server run the following command:

   ``curl -k -u admin:admin https://10.1.1.245/mgmt/shared/iapp/global-installed-packages | jq .``

   Response:

   .. code::

      {
        "items": [],
        "generation": 0,
        "kind": "shared:iapp:global-installed-packages:installedpackagecollectionstate",
        "lastUpdateMicros": 0,
        "selfLink": "https://localhost/mgmt/shared/iapp/global-installed-packages"
      }

#. We can see here that no RPM has been installed on this system.

Task 2 - Install our RPM
^^^^^^^^^^^^^^^^^^^^^^^^

Installation is performed via the iControl REST API
``package-management-tasks`` service. Performing an HTTP ``POST`` to this
service with the ``INSTALL`` operation, the location and the name of the
iControl LX package is all that is necessary to install it.

Here is the syntax:

.. code::

   POST /mgmt/shared/iapp/package-management-tasks
   {
    "operation": "INSTALL",
    "packageFilePath": "/var/config/rest/downloads/HelloWorld-0.1-001.noarch.rpm"
   }

Perform the following steps to complete this task:


#. From your Xubuntu Server run the following command:

   ``curl -H "Content-Type: application/json" -k -u admin:admin -X POST -d '{"operation": "INSTALL","packageFilePath": "/var/config/rest/downloads/HelloWorld-0.1-001.noarch.rpm"}' https://10.1.1.245/mgmt/shared/iapp/package-management-tasks | jq .``

#. The output should look like this:

   .. code::

      {
        "packageFilePath": "/var/config/rest/downloads/HelloWorld-0.1-001.noarch.rpm",
        "operation": "INSTALL",
        "id": "4d62ae98-5302-41ee-8057-479b28372b9f",
        "status": "CREATED",
        "userReference": {
         "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "identityReferences": [
         {
           "link": "https://localhost/mgmt/shared/authz/users/admin"
         }
        ],
        "ownerMachineId": "2865e578-0460-44f4-910a-8dc7f220fce1",
        "generation": 1,
        "lastUpdateMicros": 1508331598385044,
        "kind": "shared:iapp:package-management-tasks:iapppackagemanagementtaskstate",
        "selfLink": "https://localhost/mgmt/shared/iapp/package-management-tasks/4d62ae98-5302-41ee-8057-479b28372b9f"
      }

#. Note the ``id``. If you now query the ``package-managment-tasks`` resource
   and append the ``id``, you can view the status of the install.

   From your terminal:

   ``curl -k -u admin:admin  https://10.1.1.245/mgmt/shared/iapp/package-management-tasks/4d62ae98-5302-41ee-8057-479b28372b9f | jq .``

   .. NOTE::  Once again be sure to replace the ID in the curl command
      (``4d62ae98-5302-41ee-8057-479b28372b9f``) with your own ``id``

   Output:

   .. code::

      {
        "packageFilePath": "/var/config/rest/downloads/HelloWorld-0.1-001.noarch.rpm",
        "packageName": "HelloWorld-0.1-001.noarch",
        "operation": "INSTALL",
        "packageManifest": {
          "tags": [
            "IAPP"
          ]
        },
        "id": "4d62ae98-5302-41ee-8057-479b28372b9f",
        "status": "FINISHED",
        "startTime": "2017-10-18T14:59:58.389+0200",
        "endTime": "2017-10-18T14:59:58.897+0200",
        "userReference": {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "identityReferences": [
          {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
          }
        ],
        "ownerMachineId": "2865e578-0460-44f4-910a-8dc7f220fce1",
        "generation": 3,
        "lastUpdateMicros": 1508331598896783,
        "kind": "shared:iapp:package-management-tasks:iapppackagemanagementtaskstate",
        "selfLink": "https://localhost/mgmt/shared/iapp/package-management-tasks/4d62ae98-5302-41ee-8057-479b28372b9f"
      }

#. Check the status field in the output to see if the installation completed as
   expected. If the package is already installed, you will see ``FAILED``. For
   example:

   .. code::

      {
        "packageFilePath": "/var/config/rest/downloads/HelloWorld-0.1-001.noarch.rpm",
        "packageName": "HelloWorld-0.1-001.noarch.rpm",
        "operation": "INSTALL",
        "step": "INSTALL_PACKAGE",
        "id": "4d62ae98-5302-41ee-8057-479b28372b9f",
        "status": "FAILED",
        "startTime": "2017-10-18T20:06:32.879-0700",
        "endTime": "2017-10-18T20:06:33.184-0700",
        "errorMessage": "Failed to install /var/config/rest/downloads/HelloWorld-0.1-001.noarch.rpm - \tpackage HelloWorld-0.1-001.noarch is already installed",
        "userReference": {
          "link": "https://localhost/mgmt/shared/authz/users/admin"
        },
        "identityReferences": [
          {
            "link": "https://localhost/mgmt/shared/authz/users/admin"
          }
        ],
        "ownerMachineId": "2865e578-0460-44f4-910a-8dc7f220fce1",
        "generation": 4,
        "lastUpdateMicros": 1494471993184210,
        "kind": "shared:iapp:package-management-tasks:iapppackagemanagementtaskstate",
        "selfLink": "https://localhost/mgmt/shared/iapp/package-management-tasks/4d62ae98-5302-41ee-8057-479b28372b9f"
      }

#. You can check the installation by:

   * Viewing the contents of the folder ``/var/config/rest/iapps/`` on the BIG-IP:

     .. code::

        $ ls /var/config/rest/iapps/
        HelloWorld  RPMS

   * Checking the output of the command (from your Xubuntu Server):

     ``curl -k -u admin:admin https://10.1.1.245/mgmt/shared/iapp/global-installed-packages | jq .``

     You should see something like this:
     
     .. code::

        {
          "items": [
            {
              "id": "68e109f0-f40c-372a-95e0-5cc22786f8e6",
              "appName": "HelloWorld",
              "packageName": "HelloWorld-0.1-001.noarch",
              "version": "0.1",
              "release": "001",
              "arch": "noarch",
              "tags": [
                "IAPP"
              ],
              "generation": 1,
              "lastUpdateMicros": 1508331598882884,
              "kind": "shared:iapp:global-installed-packages:installedpackagestate",
              "selfLink": "https://localhost/mgmt/shared/iapp/global-installed-packages/68e109f0-f40c-372a-95e0-5cc22786f8e6"
            }
          ],
          "generation": 1,
          "kind": "shared:iapp:global-installed-packages:installedpackagecollectionstate",
          "lastUpdateMicros": 1508331598883142,
          "selfLink": "https://localhost/mgmt/shared/iapp/global-installed-packages"
        }

#. You can also check your restnoded.log file:

   .. code::

      $ tail -10 /var/log/restnoded/restnoded.log

      Wed, 18 Oct 2017 13:27:21 GMT - finest: socket 1 opened
      Wed, 18 Oct 2017 13:27:21 GMT - finest: socket 2 opened
      Wed, 18 Oct 2017 13:27:21 GMT - finest: socket 1 closed
      Wed, 18 Oct 2017 13:27:21 GMT - finest: [LoaderWorker] triggered at path:  /var/config/rest/iapps/HelloWorld/nodejs
      Wed, 18 Oct 2017 13:27:21 GMT - finest: socket 2 closed
      Wed, 18 Oct 2017 13:27:21 GMT - finest: [LoaderWorker] triggered at path:  /var/config/rest/iapps/HelloWorld/nodejs/hello_world.js
      Wed, 18 Oct 2017 13:27:21 GMT - info: DEBUG: HelloWorld - onStart request
      Wed, 18 Oct 2017 13:27:21 GMT - config: [RestWorker] /ilxe_lab/hello_world has started. Name:HelloWorld
     Wed, 18 Oct 2017 13:27:21 GMT - info: DEBUG: HelloWorld - onStart - the default message body is: { "value": "Congratulations on your lab!" }

#. We can see here that our iControl LX Extension has been added to ``restnoded``.

Task 3 - Test our iControl Extension
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. You can simply redo some of our previous tests to see the outcome:

   ``curl -k -u admin:admin https://10.1.1.245/mgmt/ilxe_lab/hello_world``

#. The console output should look like this:

   ``{"value":"Congratulations on your lab!"}``

#. Execute ``curl -H "Content-Type: application/json" -k -u admin:admin -X POST -d '{"name":"iControl LX Lab"}' https://10.1.1.245/mgmt/ilxe_lab/hello_world``

   The console output should look like this:

   ``{"value":"Hello iControl LX Lab!"}``

#. Execute ``curl -H "Content-Type: application/json" -k -u admin:admin -X POST -d '{"other":"iControl LX Lab"}' https://10.1.1.245/mgmt/ilxe_lab/hello_world``

#. The console output should look like this (the name parameter wasn't found in
   the POST payload):

   ``{"value":"Congratulations on your lab!"}``

