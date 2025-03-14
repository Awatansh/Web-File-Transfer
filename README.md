# Simple File Server

This is a basic TCP file server implemented in C using the socket API. It listens for incoming connections and sends the requested file to the client.

## How It Works
1. Creates a TCP socket.
2. Binds to port `8080` (0x901f in hex, which is little-endian for 8080).
3. Listens for incoming connections.
4. Accepts a client connection.
5. Reads the client's request (expects an HTTP-like request format: `GET /filename`).
6. Extracts the requested filename and attempts to open it.
7. Sends the file's contents back to the client.
8. Closes the connection.

## Prerequisites
- A Linux-based system with GCC installed.
- Basic understanding of sockets and system calls.

## Compilation
Compile the server using:
```sh
gcc -o file_server file_server.c
```

## Usage
Run the server:
```sh
./file_server
```
Then, from another terminal, request a file using `wget`:
```sh
wget -O downloaded_file.txt http://localhost:8080/testfile.txt
```

## Notes
- The server expects a request in the format `GET /filename`.
- It does not handle HTTP responses properly and sends only raw file data.
- The buffer size for `sendfile` is limited to 256 bytes, which may not work well for larger files.
- This implementation lacks error handling for invalid or missing files.

## Disclaimer
This is a minimal implementation and should not be used in production. It lacks security measures such as input validation and proper error handling.

