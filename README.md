# Chat System Using RAFT (Distributed & Fault-Tolerant)

A distributed, highly available chat application that utilizes the **Raft Consensus Algorithm** to maintain a secure, replicated log of encrypted messages across decentralized clients. 

This system ensures that chat logs remain consistent, ordered, and resilient against network partitions or node failures, eliminating the reliance on a single centralized server database.

##  Key Features

* **Raft-Backed Replicated Log**: Guaranteed fault tolerance and strict message ordering across active nodes.
* **Dynamic Group Membership**: Secure protocols for clients to seamlessly join or leave isolated group chats.
* **End-to-End Privacy**: Messages are fully encrypted; only authenticated members within a specific group can access or decrypt historical and live logs.
* **High Availability**: Continuous service availability as long as a majority quorum of client nodes remains online.

##  System Architecture

* **Consensus Engine**: Raft (Leader Election, Log Replication, Safety)
* **Communication Layer**: Sockets (Python)

##  Cryptographic Security Model (Hybrid Encryption)

To balance high-throughput performance with strict group isolation, the system implements a **Hybrid Cryptosystem** over the Raft replication layer:

*   **Group Communication (Symmetric Engine)**: All message payloads written to the distributed Raft log are encrypted using a shared symmetric key unique to that specific group. This ensures minimal processing overhead during high-frequency log replication.
*   **Group Access Control (Asymmetric Gateway)**: Membership authorization is enforced via asymmetric cryptography. When a client requests to join a group, the shared symmetric group key is securely wrapped using the client's individual public encryption key. The client then utilizes their distinct, localized private decryption key to unlock the group key and gain access to the text stream.

---
*Course Project for CS271 (Winter 2022). For the complete design prompt, see the [Project Specification PDF](CS271_Final_Project__W22_1.pdf).*
