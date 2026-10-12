# 🚀 DHCP Server-Client Simulation using UDP Socket Programming (C)
 
A **DHCP (Dynamic Host Configuration Protocol)** Server-Client simulation developed in **C using UDP Socket Programming**. This project demonstrates how a DHCP server dynamically assigns IP addresses to clients through the standard **4-step DHCP handshake**, along with **lease management**, **lease expiration checking**, and **dynamic IP allocation**.

The project is ideal for learning:

* Computer Networks
* Socket Programming
* Client–Server Architecture
* Operating Systems
* Linux System Programming

---

# 📚 Table of Contents

* Project Overview
* Key Highlights
* Technologies Used
* Features
* Project Structure
* System Architecture
* Internal Architecture
* Overall Workflow
* Client Workflow
* Server Workflow
* DHCP Handshake
* Lease Table
* Lease Expiration
* IP Allocation Algorithm
* Sequence Diagram
* Compilation
* Execution
* Sample Output
* Concepts Demonstrated
* Future Improvements
* Learning Outcomes
* Author

---

# 📖 Project Overview

DHCP (Dynamic Host Configuration Protocol) automatically assigns IP addresses to devices joining a network. Instead of configuring every client manually, the DHCP server maintains a pool of available IP addresses and dynamically allocates one whenever a client requests network access.

This project simulates the complete DHCP workflow using **UDP Socket Programming** in C.

The implementation includes:

* DHCP Discover
* DHCP Offer
* DHCP Request
* DHCP ACK
* Dynamic IP Allocation
* Lease Table Management
* Lease Expiration Checking
* Transaction ID Verification
* Broadcast Communication

---

# ⭐ Key Highlights

* Dynamic IP Allocation
* Complete DHCP 4-Step Handshake
* UDP Socket Programming
* Client–Server Architecture
* Lease Table Management
* Lease Expiration Checking
* IP Pool Management
* Transaction ID Verification
* Broadcast Communication
* Linux Socket API

---

# 🛠 Technologies Used

| Component            | Description      |
| -------------------- | ---------------- |
| **Language**         | C                |
| **Protocol**         | DHCP             |
| **Transport Layer**  | UDP              |
| **Socket API**       | Linux Socket API |
| **Compiler**         | GCC              |
| **Operating System** | Linux            |

---

# ✨ Features

* ✔ DHCP Discover
* ✔ DHCP Offer
* ✔ DHCP Request
* ✔ DHCP ACK
* ✔ Dynamic IP Allocation
* ✔ Lease Time Management
* ✔ Lease Expiration Checking
* ✔ Lease Table Management
* ✔ Transaction ID Verification
* ✔ Broadcast Communication
* ✔ UDP Client–Server Architecture
* ✔ Multiple Lease Entries

---

# 📂 Project Structure

```text
DHCP-server-client-main/
│
├── DHCPserver.c
│     ├── Socket Creation
│     ├── Lease Table Management
│     ├── DHCP Offer
│     ├── DHCP ACK
│     ├── IP Allocation
│     └── Lease Expiration Checking
│
├── DHCPclient.c
│     ├── UDP Socket Creation
│     ├── DHCP Discover
│     ├── Receive Offer
│     ├── DHCP Request
│     └── Receive ACK
│
└── README.md
```

---

# 🏗 System Architecture

```text
             +----------------------+
             |     DHCP Client      |
             +----------+-----------+
                        |
                        |
               DHCP Discover
                        |
                        ▼
             +----------+-----------+
             |     DHCP Server      |
             +----------+-----------+
                        |
              Search Available IP
                        |
                        ▼
                 Allocate Lease
                        |
                        |
                 DHCP Offer
                        |
                        ▼
             +----------+-----------+
             |     DHCP Client      |
             +----------+-----------+
                        |
                 DHCP Request
                        |
                        ▼
             +----------+-----------+
             |     DHCP Server      |
             +----------+-----------+
                        |
                  DHCP ACK
                        |
                        ▼
             Client Receives IP
```

---

# ⚙ Internal Architecture

```text
                DHCP SERVER

        +------------------------+
        | UDP Socket             |
        +------------------------+
                    |
                    ▼
        +------------------------+
        | Receive Discover       |
        +------------------------+
                    |
                    ▼
        +------------------------+
        | Check Lease Table      |
        +------------------------+
                    |
                    ▼
        +------------------------+
        | Lease Expired ?        |
        +------------------------+
             |            |
            Yes          No
             |            |
             ▼            ▼
      Free Expired IP  Continue
             |
             ▼
      Find Available IP
             |
             ▼
      Send DHCP OFFER
             |
             ▼
      Receive REQUEST
             |
             ▼
        Send DHCP ACK
```

---

# 🔄 Overall Workflow

```text
Start
   │
   ▼
Client Starts
   │
   ▼
Broadcast DHCP Discover
   │
   ▼
Server Receives Discover
   │
   ▼
Check Lease Table
   │
   ▼
Lease Expired?
   │
 ┌─┴───────────────┐
 │                 │
Yes               No
 │                 │
Free Lease     Search Free IP
 │                 │
 └──────┬──────────┘
        ▼
Allocate IP
        │
        ▼
Send DHCP Offer
        │
        ▼
Receive DHCP Request
        │
        ▼
Send DHCP ACK
        │
        ▼
Client Stores Assigned IP
        │
        ▼
Communication Completed
```

---

# 👨‍💻 Client Workflow

```text
Start Client
      │
      ▼
Create UDP Socket
      │
      ▼
Broadcast DHCP Discover
      │
      ▼
Wait for DHCP Offer
      │
      ▼
Receive Offered IP
      │
      ▼
Send DHCP Request
      │
      ▼
Receive DHCP ACK
      │
      ▼
Store Assigned IP
      │
      ▼
End
```

---

# 🖥 Server Workflow

```text
Start Server
      │
      ▼
Create UDP Socket
      │
      ▼
Bind Socket
      │
      ▼
Initialize Lease Table
      │
      ▼
Wait for Discover
      │
      ▼
Check Lease Expiration
      │
      ▼
Search Available IP
      │
      ▼
Send DHCP Offer
      │
      ▼
Receive DHCP Request
      │
      ▼
Update Lease Table
      │
      ▼
Send DHCP ACK
      │
      ▼
Wait for Next Client
```

---

# 🤝 DHCP 4-Step Handshake

```text
Client                               Server

  |                                     |

  |----- DHCP DISCOVER ----------------->|

  |                                     |

  |<------ DHCP OFFER ------------------|

  |                                     |

  |----- DHCP REQUEST ----------------->|

  |                                     |

  |<------- DHCP ACK -------------------|

  |                                     |

Connection Established
```

---

# 📋 Lease Table

The server maintains a lease table that stores:

* Assigned IP Address
* Lease Start Time
* Lease Duration
* Lease Status
* Client Information

Example:

```text
+-----------------------------------------------+
| IP Address     | Active | Lease Time         |
+-----------------------------------------------+
|192.168.10.1    | Yes    | 3600 sec           |
|192.168.10.2    | No     | ---                |
|192.168.10.3    | Yes    | 3600 sec           |
+-----------------------------------------------+
```

---

# ⏱ Lease Expiration

Before assigning a new IP address, the server checks all active leases.

If a lease has exceeded the configured **LEASE_DURATION**, the server:

* Marks the lease as expired
* Releases the IP address
* Returns it back to the IP pool
* Makes it available for future clients

Workflow:

```text
Receive Discover
        │
        ▼
Check Lease Expiration
        │
        ▼
Lease Expired?
      │        │
     Yes      No
      │        │
Free IP     Continue
      │
      ▼
Assign Available IP
```

---

# 📡 IP Allocation Algorithm

```text
Receive Discover
       │
       ▼
Check Lease Table
       │
       ▼
Existing Lease?
   │            │
  Yes          No
   │            │
Return Same IP Find Free IP
                │
                ▼
         IP Available?
          │         │
         Yes       No
          │         │
     Assign IP   Reject Request
```

---

# 📊 Sequence Diagram

```text
Client                         Server

Start
 |
 |------ Discover ------------>|
 |                              |
 |                              | Check Lease Table
 |                              | Check Lease Expiration
 |<------ Offer ---------------|
 |
 |------ Request ------------->|
 |                              |
 |                              | Allocate Lease
 |<------ ACK -----------------|
 |
Communication Ends
```

---

# ⚡ Compilation

Compile Server

```bash
gcc DHCPserver.c -o DHCPserver
```

Compile Client

```bash
gcc DHCPclient.c -o DHCPclient
```

---

# ▶ Execution

Run Server

```bash
./DHCPserver 5000
```

Run Client

```bash
./DHCPclient 5000
```

---

# 🖥 Sample Output

### Server

```text
DHCP Server Started

DISCOVER Received

Checking Lease Table...

Offering IP : 192.168.10.2

REQUEST Received

ACK Sent

Lease Created Successfully
```

### Client

```text
DHCP Client Started

Broadcasting DHCP Discover...

DHCP Offer Received

Assigned IP:
192.168.10.2

Sending DHCP Request...

ACK Received

Lease Time:
3600 seconds
```

---

# 📚 Concepts Demonstrated

* DHCP Protocol
* UDP Socket Programming
* Client–Server Architecture
* Dynamic IP Allocation
* Lease Management
* Lease Expiration
* Broadcast Communication
* Transaction IDs
* Linux Socket Programming
* Network Programming
* Computer Networks
* Operating Systems

---

# 🚀 Future Improvements

* Multi-client Support using Threads
* DHCP Release
* DHCP Renew
* DHCP NAK Support
* Persistent Lease Storage
* Configuration File
* Logging System
* IPv6 Support
* Packet Sniffer Integration
* GUI Dashboard
* Automatic Background Lease Monitoring
* DHCP Relay Agent Simulation

---

# 🎯 Learning Outcomes

After completing this project, you will understand:

* DHCP Protocol
* UDP Socket Programming
* Client–Server Communication
* Dynamic IP Assignment
* Lease Management
* Lease Expiration
* Linux Socket API
* Broadcast Networking
* System Programming
* Computer Network Fundamentals

---

# 💡 Why This Project?

This project provides practical exposure to networking concepts by implementing a simplified DHCP protocol. It demonstrates how devices automatically obtain IP addresses using UDP communication while introducing concepts such as lease management, IP allocation, and client–server communication.

It is highly suitable for students preparing for interviews in:

* Computer Networks
* Operating Systems
* System Programming
* Network Programming

---

# 👨‍💻 Author

**Akhil Kumar Singh**

**B.Tech (Computer Science Engineering)**

### Skills Demonstrated

* C Programming
* UDP Socket Programming
* DHCP Protocol
* Computer Networks
* Linux System Programming
* Client–Server Architecture
* Operating Systems

---

⭐ **If you found this project useful, consider giving it a Star on GitHub!**
