# Description

This project is a simple HTTP server implemented in Rust using the standard library (std). It creates a thread pool to handle incoming TCP connections concurrently. Below is an explanation of the code:

## Imports and Main Function

The initial part of the code imports necessary modules and defines the main function.
- `std::fs`: Filesystem operations.
- `std::io::prelude::*`: I/O traits and utilities.
- `std::net::TcpListener`: TCP listener for incoming connections.
- `std::net::TcpStream`: TCP stream for reading/writing data.
- `std::thread`: Thread-related functionalities.
- `std::time::Duration`: Time-related utilities.
- `server::ThreadPool`: Custom thread pool implementation.

## Main Function

- Binds the server to `127.0.0.1:7878`.
- Creates a thread pool with 4 threads (`ThreadPool::new(4)`).
- Accepts incoming TCP connections in a loop and dispatches them to the thread pool for handling (`pool.execute(|| { handle_connection(stream); });`).

## Handle Connection Function

Handles each TCP connection.
- Reads data from the client into a buffer.
- Parses the HTTP request to determine the requested resource.
- Generates an appropriate HTTP response based on the request.

## Custom ThreadPool Implementation

Defines a custom thread pool (`struct ThreadPool`) to manage worker threads.
- Uses a message passing mechanism (`mpsc::channel`) to communicate between the main thread and worker threads.
- Workers (`struct Worker`) listen for incoming jobs (closures) and execute them concurrently.
