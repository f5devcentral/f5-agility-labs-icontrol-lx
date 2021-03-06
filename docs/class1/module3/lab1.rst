Lab 3.1 - Review the HelloWorld iControl LX Extension
-----------------------------------------------------

iControl LX Extensions are provided as RPM (RedHat Package Manager) files.  An RPM is similar to a ``.tar`` or ``.zip`` file for installing application files.

Let's begin by reviewing the JavaScript contents of the HelloWorld RPM. 
In this module we will be reviewing the contents of an extension. In the next module we will be creating our own.

Overview of the HelloWorld Extension
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To help us get started we've kept this extension very simple:

#. It only supports HTTP ``GET`` requests.
#. It only responds to ``GET`` requests with ``Hello World!``.
#. There are *only* 13 lines of JavaScript (the rest are comments and documentation).

The JavaScript code for the HelloWorld extension is as follows:

.. code-block:: javascript
   :linenos:

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


Key Parts of the HelloWorld Extension
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

WORKER_URI_PATH
~~~~~~~~~~~~~~~

Note the following line:

``HelloWorld.prototype.WORKER_URI_PATH = "ilxe_lab/hello_world";``

This specifies where the iControl LX Extension will appear within iControl REST.
Adding the ``/mgmt`` prefix, this would result in:

``https://10.1.1.245/mgmt/ilxe_lab/hello_world``


isPublic
~~~~~~~~

By default, the ``WORKER_URI_PATH`` would only be accessible to other
extensions. To make it accessible to remote devices/systems, you must specify
that it should be publicly available using:

``HelloWorld.prototype.isPublic = true;``

Accepting an HTTP GET transaction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To process an HTTP ``GET`` sent to the ``WORKER_URI_PATH`` you must use
``onGet`` as follows:

.. code-block:: javascript
   :linenos:

   HelloWorld.prototype.onGet = function(restOperation) {
     restOperation.setBody(JSON.stringify( { value: "Hello World!" } ));
     this.completeRestOperation(restOperation);
   };

This function performs the following actions:

- Accepts the HTTP ``GET`` sent to our ``WORKER_URI_PATH`` (``/mgmt/ilxe_lab/hello_world``)
- Sets the body of the response to ``{ value: "Hello World!" }``
- Completes the transaction by sending the response back to the client

iControl LX Example Transaction
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This is a special service that will come in handy in the next lab.
If you have an iControl LX Extension that supports an HTTP ``POST``, ``PATCH``,
or ``PUT``, then the client will need to know what data to send and in what
format.

The ``getExampleState`` function responds when the user appends ``/example`` to
the end of the ``WORKER_URI_PATH`` (``/mgmt/ilxe_lab/hello_world/example``):

.. code-block:: javascript
   :linenos:

   HelloWorld.prototype.getExampleState = function () {
     return {
     "value": "your_string"
     };
   };

As our ``HelloWorld`` extension does not require any inputs we haven't put in
any data here.

.. NOTE:: ``/example`` must always be used with an HTTP ``GET``.
