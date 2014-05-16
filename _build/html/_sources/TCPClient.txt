TCPClient Objects
*****************

The ``TCPClient`` class provides a concise interface for connecting and speaking to a ``TCPServer`` instance.

TCPClient([host, port])
-----------------------

Instantiates a ``TCPClient`` object.
    - ``host``: The host the target server is listening on.  Defaults to localhost.
    - ``port``: The port the target server is listening on.  Defaults to 7272.

connect()
---------

Connects to the server.

.. note::
   Available in v0.0.5 or higher.  For prior versions, use ``self.conn.connect()``

send(data)
----------

Sends the given data to the server.

recv()
------

Receives data from the server and returns them.

disconnect()
------------

Closes a connection to the server.

.. note::
   Available in v0.0.5 or higher.  For prior versions, use ``self.conn.finish()``

execute(cmd[, **params])
------------------------

Calls the server to execute the given command and returns the result.
