TCPY Tutorial
*************

**tcpy** makes it extremely simple to make TCP Servers and associated clients in Python.

Associate a command to a TCPHandler, define its execute() method and tcpy has you up and running::

    # Server
    from tcpy import TCPServer, TCPHandler

    # Our handler class must inherit from TCPHandler
    class AdditionHandler(TCPHandler):
        def __init__(self, x, y):
            # Capture parameters as members of the class
            self.x = x
            self.y = y

        def execute(self):
            # success() will provide a well-formed success response
            return self.success(solution=self.x + self.y)

    # Instantiate the server at default localhost:7272
    server = TCPServer()
    server.commands = {
        # Associate a command to our handler
        'add': AdditionHandler
    }

    if __name__ == "__main__":
        # Start listening for requests!
        server.listen()

On the client side, just execute() one of the server's commands::

    # Client
    from tcpy import TCPClient

    print TCPClient().execute(cmd="add", x=1, y=2)

Which outputs: ``{'solution': 3, 'success': True}``.
