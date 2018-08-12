Lab 4.1 - Creating the HelloWorld iControl LX Extension
-------------------------------------------------------

iControl LX Extensions are distributed as RPMs (RedHat Package Management
system) when you want to leverage something existing. However when you start
from scratch, you'll need to create your extension and then build a RPM that
you can distribute accordingly.

Task 1 - Create our iControl LX Extension on BIG-IP
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

iControl LX Extensions can be installed on either the BIG-IP or iWorkflow
platform. For this lab, we will use BIG-IP.

Perform the following steps to complete this task:

#. Connect to your BIG-IP via SSH/PuTTY(``10.1.1.245``).


#. iControl LX Extensions reside in ``/var/config/rest/iapps/``. This is where
   you need to create your iControl LX Extension. Usually you will create:

   * A folder that is the name of your app: ``HelloWorld``

   .. NOTE:: This folder name is important since this is what will be used as
      the RPM name when we will create our package later.

   * Inside the app folder, another folder called ``nodejs`` that will contain
     your extension

#. Let's create our directory tree. On your BIG-IP execute the following:

   ``mkdir -p /var/config/rest/iapps/HelloWorld/nodejs/``

#. Now that we have our directory, we need to create our extension. Use your
   preferred text editor and create a file named ``hello_world.js`` in
   ``/var/config/rest/iapps/HelloWorld/nodejs/``:

   For example, using nano the command would be ``nano /var/config/rest/iapps/HelloWorld/nodejs/hello_world.js``

   .. NOTE:: If you have not used nano before:  After you paste in the contents below, you will type ``CTRL-X`` to exit the editor.  You will then be prompted to save the file, type ``Y`` to confirm.

#. Copy/Paste the following content into your file:

   .. code-block:: javascript

      /**
      * A simple iControl LX Extension that handles only HTTP GET
      */
      function HelloWorld() {}

      HelloWorld.prototype.WORKER_URI_PATH = "ilxe_lab/hello_world";
      HelloWorld.prototype.isPublic = true;

      /**
      * handle onGet HTTP request
      */
      HelloWorld.prototype.onGet = function(restOperation) {
        restOperation.setBody(JSON.stringify( { value: "Hello World!" } ));
        this.completeRestOperation(restOperation);
      };

      /**
      * handle /example HTTP request
      */
      HelloWorld.prototype.getExampleState = function () {
        return {
          "value": "your_string"
        };
      };

      module.exports = HelloWorld;

#. Save the changes (``CTRL-X``, ``Y`` if you use ``nano``, ``ESC ESC :wq`` if you use ``vi``).

#. Once our extension is created, we need to load it into ``restnoded``. When
   an extension is loaded from an RPM, it is done automatically. However in this case
   we will need to do it ourselves.

   Use the following command on the BIG-IP to make ``restnoded`` aware of our
   extension:

   ``restcurl shared/nodejs/loader-path-config -d '{"workerPath": "/var/config/rest/iapps/HelloWorld"}'``

   .. NOTE:: ``restcurl`` is a utility that allows you to communicate with iControl REST via the CLI.

   The output should look like this:

   .. code::

     $ restcurl shared/nodejs/loader-path-config -d '{"workerPath": "/var/config/rest/iapps/HelloWorld"}'
     {
       "id": "ad130c79-59a0-49c7-a7e7-ff39efe956b5",
       "workerPath": "/var/config/rest/iapps/HelloWorld",
       "generation": 1,
       "lastUpdateMicros": 1508242306312732,
       "kind": "shared:nodejs:loader-path-config:loaderpathstate",
       "selfLink": "https://localhost/mgmt/shared/nodejs/loader-path-config/ad130c79-59a0-49c7-a7e7-ff39efe956b5"
     }

#. The logfile ``/var/log/restnoded/restnoded.0.log`` will give you the ability to track
   whether your extension is loaded as expected. Run the following command to
   ensure everything went smoothly:

   ``grep HelloWorld /var/log/restnoded/restnoded.log``

   The output should look like this:

   .. code::

      Tue, 17 Oct 2017 12:11:46 GMT - finest: [LoaderWorker] triggered at path:  /var/config/rest/iapps/HelloWorld
      Tue, 17 Oct 2017 12:11:46 GMT - finest: [LoaderWorker] triggered at path:  /var/config/rest/iapps/HelloWorld/nodejs
      Tue, 17 Oct 2017 12:11:46 GMT - finest: [LoaderWorker] triggered at path:  /var/config/rest/iapps/HelloWorld/nodejs/hello_world.js
      Tue, 17 Oct 2017 12:11:46 GMT - config: [RestWorker] /ilxe_lab/hello_world has started. Name:HelloWorld

Task 2 - Check our iControl LX Extension is Working
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Perform the following steps to complete this task:

#. In your web browser, navigate to ``https://10.1.1.245/mgmt/ilxe_lab/hello_world``.

#. You should see something like this:

   .. image:: ../../_static/class1/module4/lab1-image001.png
      :align: center
      :scale: 50%

#. You could also use ``curl`` from a command line (from the BIG-IP CLI for example):

   ``curl -k -u admin:admin https://10.1.1.245/mgmt/ilxe_lab/hello_world``

   Or a REST client like Postman.

#. Another test is to connect to our ``/example`` uri. Navigate with your
   browser to ``https://10.1.1.245/mgmt/ilxe_lab/hello_world/example``.

#. You should see something like this:

   .. image:: ../../_static/class1/module4/lab1-image002.png
      :align: center
      :scale: 50%

#. You can use ``curl`` from a command line for this as well:

   ``curl -k -u admin:admin https://10.1.1.245/mgmt/ilxe_lab/hello_world/example``

.. NOTE:: You may not want to use admin privileges to leverage an extension.
   In many situations an extension may only be needed by specific users, in which case you would be able to enforce RBAC (Role-Based Access Control) policies. BIG-IP version 13.1 and later provides this capability.

