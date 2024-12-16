# **Distributed File Storage System**

A distributed system for storing, retrieving, and managing files by dividing them into chunks and distributing these chunks across multiple nodes. This project demonstrates scalability, fault tolerance, and efficient file management, making it suitable for use cases such as cloud storage, content delivery networks (CDNs), and backup systems.

---

## **Table of Contents**
1. [Features](#features)  
2. [Architecture](#architecture)  
3. [Technologies Used](#technologies-used)  
4. [Getting Started](#getting-started)  
   - [Prerequisites](#prerequisites)  
   - [Setup](#setup)  
5. [Usage](#usage)  
   - [Upload a File](#upload-a-file)  
   - [Retrieve a File](#retrieve-a-file)  
6. [Endpoints](#endpoints)  
7. [Future Enhancements](#future-enhancements)  
8. [Contributors](#contributors)

---

## **Features**
- **File Chunking**: Files are divided into smaller chunks for distribution.
- **Distributed Storage**: Chunks are distributed across multiple server nodes using round-robin allocation.
- **Fault Tolerance**: Redundancy ensures data availability even in the event of node failures.
- **Scalability**: New nodes can dynamically join the system without requiring reconfiguration.
- **Efficient File Retrieval**: Reassembles the original file from distributed chunks.
- **Heartbeat Monitoring**: Middleware tracks active servers through periodic heartbeats.

---

## **Architecture**
The system comprises three main components:
1. **Client**:  
   - Provides a user interface to upload and retrieve files.  
   - Communicates with the middleware via HTTP requests.  
2. **Middleware**:  
   - Coordinates chunk distribution and tracks active servers.  
   - Provides endpoints for file upload, retrieval, and server registration.  
3. **Server Nodes**:  
   - Store file chunks and share them with peer nodes for redundancy.  
   - Send periodic heartbeats to middleware to indicate availability.  

![Basic Architecture Diagram](https://github.com/user-attachments/assets/beca3f66-6dcd-41f2-8bf2-56aefc6b4200)


---

## **Technologies Used**
- **Frontend**: HTML, JavaScript
- **Backend**: Node.js, Express.js
- **Libraries**:  
  - `multer`: For handling file uploads.  
  - `axios`: For making HTTP requests between middleware and servers.  
  - `mime-types`: For determining file types during retrieval.  
  - `fs` and `path`: For file and directory operations.

---

## **Getting Started**

### **Prerequisites**
- Node.js (v16 or later)
- npm (Node Package Manager)
- Basic knowledge of Node.js and REST APIs.

### **Setup**
1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/distributed-file-storage.git
   cd distributed-file-storage
   ```

2. Install dependencies for all components:
   ```bash
   npm install
   ```

3. Start the middleware server:
   ```bash
   cd middleware
   node index.js
   ```

4. Start multiple server nodes:
   ```bash
   cd server
   node server.js
   ```

5. Launch the client by opening `client.html` in a browser.

---

## **Usage**

### **Upload a File**
1. Open the **client interface** in your browser.
2. Select a file using the "Choose File" button.
3. Click the "Upload" button.  
   - The middleware will divide the file into chunks and distribute them across server nodes.  
   - A unique `File ID` will be displayed upon successful upload.  

### **Retrieve a File**
1. Enter the `File ID` in the text box provided in the client interface.
2. Click the "Retrieve" button.  
   - The middleware will reassemble the file from its chunks and prompt the user to download it.

---

## **Endpoints**

### **Middleware**
| Endpoint                 | Method | Description                                             |
|--------------------------|--------|---------------------------------------------------------|
| `/update-server-url`     | POST   | Registers or updates a server's URL.                   |
| `/upload`                | POST   | Uploads a file, splits it into chunks, and distributes. |
| `/retrieve/:fileId`      | GET    | Retrieves a file by its unique File ID.                |
| `/server-list`           | GET    | Returns a list of active server nodes.                 |

### **Server**
| Endpoint            | Method | Description                                      |
|---------------------|--------|--------------------------------------------------|
| `/store-chunk`      | POST   | Stores a file chunk locally.                     |
| `/share-chunk`      | POST   | Shares a file chunk with other servers.          |
| `/get-chunk/:fileId/:index` | GET    | Retrieves a specific chunk by file ID and index. |

---

## **Future Enhancements**
- **Authentication and Security**: Add user authentication and encrypt file chunks for secure storage.
- **Load Balancing**: Implement intelligent load balancing for chunk distribution.
- **Dynamic Replication**: Adjust the number of replicas dynamically based on server availability.
- **Monitoring Dashboard**: Build a UI to monitor server statuses and file distribution.

---

## **Contributors**
- **Abdul Malik**: Middleware Development, Chunk Distribution  
- **Vishwa**: Client and Server Development, Fault Tolerance  

Feel free to contribute! Fork the repository, create a new branch, and submit a pull request with your proposed changes.

---
