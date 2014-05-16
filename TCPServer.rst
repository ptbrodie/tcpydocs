TCPServer Objects
*****************

The ``TCPServer`` class handles accepting requests and queuing tasks for worker threads to complete.

``TCPServer([host, port, commands, threads, poll_intv])``
---------------------------------------------------------

   Initializes an instance of the ``TCPServer`` class.
       -``host``: the hostname where the server will live. Defaults to locahost.
       -``port``: the port on which the server will listen. Defaults to 7272.
       -``commands``: dictionary mapping command strings to handler classes.
       -``threads``: number of worker threads the server will spawn to execute tasks. Defaults to 4.
       -``poll_intv``: the period of time a worker will sleep before polling the request queue for work.

``listen()``
------------

   Tells a ``TCPServer`` object to begin listening for requests. TCPY will log the host and port where it is listening to stdout.

The TCPServer.commands Dictionary
---------------------------------

The ``commands`` dictionary of a ``TCPServer`` object is how the server knows which commands to execute.  It maps command names (strings) to handler classes.

For example::

    from tcpy import TCPServer
    from foo import FooHandler

    server = TCPServer()
    server.commands = {
        'foo': FooHandler    # maps the command 'foo' onto the FooHandler class
    }
    server.listen()

Defining commands this way allows clients to execute specific commands similar to a remote procedure call. A ``TCPClient`` may call ``execute`` on a given command, and the ``TCPServer`` will instantiate the appropriate handler class to serve the client's request.
