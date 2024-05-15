# Application Protocols

### Network Access Layer
1. **ARP (Address Resolution Protocol)**
   - **Purpose:** Find MAC addresses of devices on the same network using IP addresses.
   - **Operation:** Uses a broadcast signal (ARP request) on the LAN with the target IP address. The device with that IP replies with an ARP reply containing its MAC address. This information is cached in the sender's ARP table for future use.

2. **Ethernet**
   - **Purpose:** Defines how packets are sent and received on LANs.
   - **Operation:** Uses CSMA/CD (Carrier Sense Multiple Access with Collision Detection) to manage data transmission, checking if the medium is free before sending data to avoid collisions.

3. **WLAN (Wireless Local Area Network)**
   - **Purpose:** Connects wireless devices like smartphones, tablets, and laptops to a local network.

### Internet Layer
1. **IPv4**
   - **Purpose:** Provides addressing and routing for packets across networks.
   - **Operation:** Uses routing tables to direct packets to their destination.

2. **NAT (Network Address Translation)**
   - **Purpose:** Allows multiple devices on a local network to share a single public IP address.
   - **Operation:** Translates private IP addresses to a public IP address for outgoing traffic and vice versa for incoming traffic.

3. **IPv6**
   - **Purpose:** Provides a larger address space than IPv4.
   - **Features:** Supports automatic address configuration (SLAAC), manual configuration (RA), multicast, and anycast addressing.

4. **DHCP (Dynamic Host Configuration Protocol)**
   - **Purpose:** Automatically assigns IP addresses to devices on a network.
   - **Operation:** Devices send a DHCP request to obtain an IP address and other network configurations.

5. **ICMPv4 (Internet Control Message Protocol for IPv4)**
   - **Purpose:** Used for diagnostics and error reporting.
   - **Features:** Includes echo requests and replies (ping) and traceroute functionality.

6. **ICMPv6**
   - **Purpose:** Similar to ICMPv4 but for IPv6 networks.
   - **Features:** Includes additional functionalities like MLD (Multicast Listener Discovery) and ND (Neighbor Discovery).

### Transport Layer
1. **TCP (Transmission Control Protocol)**
   - **Purpose:** Provides reliable, connection-oriented communication.
   - **Features:** Uses acknowledgments, sequence numbers, flow control, error detection, and supports full duplex communication.

2. **UDP (User Datagram Protocol)**
   - **Purpose:** Provides fast, connectionless communication.
   - **Features:** Low overhead, supports broadcast and multicast, and is commonly used for multimedia and online gaming.

3. **3-Way Handshake (TCP Connection Establishment)**
   - **Steps:** Client sends SYN, server responds with SYN-ACK, client sends ACK.

### Application Layer
1. **DNS (Domain Name System)**
   - **Purpose:** Translates domain names to IP addresses.
   - **Features:** Uses root servers and caching to store resolved DNS records temporarily.

2. **DHCPv4 and DHCPv6**
   - **Purpose:** Automatically assigns IP addresses and network configurations to devices.
   - **DHCPv6 Features:** Introduces prefix delegation and works with SLAAC.

3. **HTTP (Hypertext Transfer Protocol)**
   - **Purpose:** Used for transmitting web pages.
   - **Features:** Stateless, supports content negotiation and caching.

4. **HTTPS (HTTP Secure)**
   - **Purpose:** Secure version of HTTP.
   - **Features:** Encrypts data using SSL/TLS for confidentiality and integrity.

5. **Email Protocols (SMTP, POP3, IMAP)**
   - **SMTP:** Sends emails, supports authentication, and secure transmission.
   - **POP3:** Retrieves emails, downloads and stores them locally.
   - **IMAP:** Manages and syncs emails across multiple devices, supports advanced folder management.

6. **FTP (File Transfer Protocol)**
   - **Purpose:** Transfers files between client and server.
   - **Features:** Uses clear-text, can be secured with FTPS.

7. **SFTP (SSH File Transfer Protocol)**
   - **Purpose:** Secure file transfer.
   - **Features:** Uses SSH for encryption, supports SSH key-based authentication.

8. **TFTP (Trivial File Transfer Protocol)**
   - **Purpose:** Simple file transfer protocol, often used in LANs.
   - **Features:** Connectionless, uses UDP, minimal security, suitable for simple requests.

### Summary
These protocols enable efficient communication and data transfer across different layers of a network, from physical connections to application-level interactions, ensuring that devices can connect, communicate, and exchange data reliably and securely.

---
# Subnetting

## Fixed Length Subnet Masking (FLSM)

### Key Concepts and Formulas

1. **Number of Subnets:**
   - Formula: \( 2^b \)
   - \( b \) = number of bits borrowed from the host part to create the subnet part.

2. **Number of Hosts per Subnet:**
   - Formula: \( 2^h - 2 \)
   - \( h \) = number of bits remaining for hosts in the subnet.
   - The subtraction of 2 accounts for the network address and the broadcast address, which cannot be assigned to hosts.

### Steps to Calculate Subnets and Hosts

1. **Identify the total number of bits in the IP address.**
   - For IPv4, it's 32 bits.

2. **Determine the default subnet mask for the given network class:**
   - Class A: Default subnet mask is 255.0.0.0 (/8)
   - Class B: Default subnet mask is 255.255.0.0 (/16)
   - Class C: Default subnet mask is 255.255.255.0 (/24)

3. **Decide on the new subnet mask based on requirements.**
   - For example, if you need to create more subnets, you borrow bits from the host portion.

4. **Calculate the number of subnets:**
   - Determine how many bits you can borrow from the host portion without leaving too few bits for hosts.
   - Use the formula \( 2^b \) where \( b \) is the number of bits borrowed.

5. **Calculate the number of hosts per subnet:**
   - Subtract the number of bits borrowed from the total bits available for hosts.
   - Use the formula \( 2^h - 2 \), where \( h \) is the remaining bits for hosts.

### Example Calculation

#### Given:

- A Class C network: 192.168.1.0/24
- We need 4 subnets.

#### Step-by-Step:

1. **Default subnet mask for Class C: /24 (255.255.255.0)**

2. **Determine the number of bits to borrow:**
   - To create 4 subnets: \( 2^b \geq 4 \)
   - \( b = 2 \) (because \( 2^2 = 4 \))

3. **New subnet mask:**
   - Original mask /24 plus 2 borrowed bits: /26
   - New subnet mask: 255.255.255.192 (/26)

4. **Calculate the number of subnets:**
   - \( 2^b = 2^2 = 4 \)

5. **Calculate the number of hosts per subnet:**
   - Remaining bits for hosts: 32 total bits - 26 subnet bits = 6 bits
   - \( 2^h - 2 = 2^6 - 2 = 64 - 2 = 62 \)
   - Each subnet can have 62 hosts.

#### Summary:

- **Number of subnets:** 4
- **Number of hosts per subnet:** 62

### Ensuring Sufficient Subnets and Hosts without Wastage

1. **Determine the total number of required subnets and hosts per subnet.**
   - Ensure the number of bits borrowed for subnets provides at least the required number of subnets.
   - Ensure the remaining bits for hosts provide at least the required number of hosts.

2. **Balance between the number of subnets and the number of hosts:**
   - If you need more subnets, you will have fewer hosts per subnet (and vice versa).
   - Borrow only the necessary number of bits to meet your subnet requirements, leaving as many bits as possible for hosts to minimize wastage.

By carefully planning the number of bits borrowed and the resulting subnet mask, you can efficiently use FLSM to create the required number of subnets and allocate the necessary number of hosts per subnet without wastage.