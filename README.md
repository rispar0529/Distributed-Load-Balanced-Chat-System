# Distributed-Load-Balanced-Chat-System

## Overview
This project implements a multithreaded chat room system designed to handle concurrent connections across multiple servers. It features a custom Load Balancer that utilizes a Dynamic Round-Robin algorithm to distribute client traffic evenly, ensuring optimal resource utilization and system stability.

The application is built using C++ and relies on TCP Socket Programming for network communication. It leverages POSIX threads (pthreads) to handle parallel client interactions and uses Mutex locks to manage race conditions and ensure thread safety during critical operations.

## Key Features
* **Distributed Architecture:** Supports simultaneous connections from multiple clients across multiple server instances.
* **Load Balancing:** Implements a Round-Robin Load Balancing technique to monitor server traffic and direct clients to the optimal server.
* **Multithreading:** Utilizes multithreading to enable parallel communication for every connected client.
* **Thread Safety:** Implements Mutex locks for each client connection to prevent race conditions.
* **Room Management:** Allows clients to join specific chat rooms via unique Room IDs.

## System Architecture
The system operates on a Client-Server model mediated by a central Load Balancer.

1.  **Connection Request:** The Client initiates a connection request to the Load Balancer, providing a client name and the desired Room ID.
2.  **Load Assessment:** The Load Balancer communicates with active servers to assess the current client load on each instance.
3.  **Traffic Distribution:** Using the Round-Robin algorithm, the Load Balancer assigns the client to the server with the least load or the next server in the queue.
4.  **Session Establishment:** The Client establishes a direct TCP connection with the assigned Server, which spawns a dedicated thread to handle message transmission.

## Installation and Setup

### Prerequisites
* Linux Operating System
* GCC Compiler (`g++`)
* Git

### Cloning the Repository
Open your terminal and clone the repository:

```bash
git clone [https://github.com/rispar0529/Distributed-Load-Balanced-Chat-System.git](https://github.com/rispar0529/Distributed-Load-Balanced-Chat-System.git)
cd Distributed-Load-Balanced-Chat-System
```

### Compilation
Compile the source files for the Server, Load Balancer, and Client using the following commands:

```bash
g++ server.cpp -lpthread -o server
g++ loadbalancer.cpp -lpthread -o loadbalancer
g++ client.cpp -lpthread -o client
```

### Usage

#### 1. Initialize Server
Open separate terminal instances for each server you intend to run. Assign a unique port number to each server. Note that ports must be consecutive (e.g., 8080, 8081).

```bash
./server <port>
```

#### 2. Initialize Load Balancer
In a new terminal instance, run the load balancer. By default, it operates on port 6000.

```bash
./loadbalancer
```

When prompted, enter the port number of the first server (e.g., 8080) and total number of servers.

#### 3, Initialize Clients
In a new terminal instance, run the client application.

```bash
./client
```
Enter Client Name and Room ID to join, and repeat this in new terminals for additional clients.

