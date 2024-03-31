# nonstop_networking

The goal is to write a client server application. The server maintains a temp directory containing files. And the client can send commands to the server GET, to get a file, PUT to save a file, DELETE to delete a file and LIST to list all the files.

The communication has to occur over a TCP/IP socket with a well defined protocol:
* For GET the protocol is:
* First the text "GET filename\n" where filename is the filename to be read
Response is
* 8 bytes containing the size of the file (little endian)
* then all the bytes of the file

* For PUT the protocol is:
* First the text "PUT filename\n", where filename is the filename to be sent
* Then 8 bytes containg the size of the file (little endian)
* Then all the bytes of the file
Response:
* "OK\n"

* for DELETE the protocol is:
* First the text "DELETE filename\n", where filename is the filename to be deleted
Response:
* "OK\n"

* for LIST the protocol is:
* first the text is "LIST\n"
Response:
* 8 bytes containin the size of the file list (little endian)
* The names of the files separated by \n characters

In all cases if there is an error in the command the response will be:
* "ERROR\n"
* followed by an error message and a \n

Files will be stored in a temp directory made with mktemp, however the server will maintain a copy of all the files in a vector.
