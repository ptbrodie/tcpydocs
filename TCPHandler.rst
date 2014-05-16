TCPHandler Objects
******************

In **tcpy**, commands are associated to handlers. A client can ask the server to execute a command, and the server will know which handler has the responsibility of carrying out that command. The ``TCPHandler`` class is the base building block for implementing handlers, which compose a ``TCPServer``'s functionality.

All **tcpy** handlers should inherit from this class and define their behavior in an ``execute()`` method.

Associating a string command to a handler class within the ``TCPServer``'s ``command`` dictionary will give the server the ability to execute the handler.

__init__(**params)
------------------

All parameters passed by a client with a request will be forwarded into the appropriate handler's ``__init__()`` method.  They should be captured here as members of the handler class.

.. note::
   In many cases a client's connection to the server will need to be maintained to communicate back and forth. Calling `super(MyHandler, self).__init__()` when initializing a handler will give the handler access to the connection to the client.

execute()
---------

Defines the behavior of a given handler. Called on a worker thread when the command associated with a given handler is requested by a client.

.. note::
   Must be implemented by subclasses of the ``TCPHandler`` class.

success([**kwargs])
-------------------

Provides a wrapper for well-formed success responses. Returns a dictionary of the form::

    {
        'success': True,
        ...      # kwargs
    }

error(message[, **kwargs])
--------------------------

Provides a wrapper for well-formed error responses. Returns a dictionary of the form::

    {
        'error': True,
        'message': message,
        ...    # kwargs
    }

send(data)
----------

Sends the given ``data`` (in dictionary form) to a client without closing the connection.

.. note::
   A handler must call it's parent's ``__init__()`` method in order to use the connection.

recv()
----------

Receives data from a connected client and returns it in dictionary form.

.. note::
   A handler must call it's parent's ``__init__()`` method in order to use the connection.
