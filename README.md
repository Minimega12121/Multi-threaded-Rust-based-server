<h1> Discription </h1> 
This project is a simple HTTP server implemented in Rust using the standard library (std). It creates a thread pool to handle incoming TCP connections concurrently.<Br>
Below is an explanation of the code:

<h2>Imports and Main Function:</h2>

The initial part of the code imports necessary modules and defines the main function.<Br>
std::fs: Filesystem operations.<Br>
std::io::prelude::*: I/O traits and utilities.<Br>
std::net::TcpListener: TCP listener for incoming connections.<Br>
std::net::TcpStream: TCP stream for reading/writing data.<Br>
std::thread: Thread-related functionalities.<Br>
std::time::Duration: Time-related utilities.<Br>
server::ThreadPool: Custom thread pool implementation .<Br>


<h2>Main Function:</h2>

Binds the server to 127.0.0.1:7878.<Br>
Creates a thread pool with 4 threads (ThreadPool::new(4)).<Br>
Accepts incoming TCP connections in a loop and dispatches them to the thread pool for handling (pool.execute(|| { handle_connection(stream); });).<Br>


<h2>Handle Connection Function:</h2>

Handles each TCP connection.<Br>
Reads data from the client into a buffer.<Br>
Parses the HTTP request to determine the requested resource.<Br>
Generates an appropriate HTTP response based on the request.<Br>

<h2>Custom ThreadPool Implementation:</h2>

Defines a custom thread pool (struct ThreadPool) to manage worker threads.<Br>
Uses a message passing mechanism (mpsc::channel) to communicate between the main thread and worker threads.<Br>
Workers (struct Worker) listen for incoming jobs (closures) and execute them concurrently.<Br>
