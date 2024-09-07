# Encrypted Chat Application

This application allows clients to communicate securely through encrypted messaging using RSA encryption for confidentiality and digital signatures for authentication. The server manages client connections and routes messages between them.

## How to Run the Program

### Step 1: Compile the Server and Client Code
Use GCC to compile the server and client programs:


- **`gcc -o server server.c -lpthread -lssl -lcrypto`**
- **`gcc -o client client.c -lpthread -lssl -lcrypto`**

### Step 2: Run the Server
Start the server, which listens for incoming client connections on port 8080:

- **`./server`**

### Step 3: Run a Client
Start a client by providing a username and the server's IP address:

- **`./client <username> <server-ip>`**

For example:
- **`./client alice 127.0.0.1`**
  The client will prompt you to enter the PEM passphrase to load the client’s private key.

### Step 4: Sending and Receiving Messages
- To send a message, use the format: **`@[recipient username] [message]`**.
- Received messages will be automatically displayed in the client terminal.

#### Required Libraries
Ensure the following libraries are installed on your system:

##### Standard Libraries:
- `<stdio.h>`
- `<stdlib.h>`
- `<string.h>`
- `<unistd.h>`
- `<pthread.h>`
- `<arpa/inet.h>`

##### OpenSSL Libraries (for encryption and signing):
- `<openssl/rsa.h>`
- `<openssl/pem.h>`
- `<openssl/err.h>`
- `<openssl/sha.h>`

##### Installation of OpenSSL:
If you are using Ubuntu or another Debian-based system, install the OpenSSL libraries with:

- `sudo apt update`
- `sudo apt install libssl-dev`

###### Design Choices:
1. **RSA Encryption**: Messages between clients are encrypted using RSA to ensure confidentiality. Only the intended recipient with the correct private key can decrypt the message.
2. **Digital Signatures**: Messages are signed using the sender's private key, allowing the recipient to verify the sender's identity and ensure message integrity.
3. **Multi-threaded Communication**: The client uses separate threads for sending and receiving messages to ensure smooth, concurrent operations.
4. **Client Registration**: Each client registers as either a sender or receiver on the server to establish a clear communication route, ensuring that messages are correctly delivered.
5. **Error Handling**: Error messages are sent when registration fails or when the intended recipient is unavailable, improving user feedback during operation.
