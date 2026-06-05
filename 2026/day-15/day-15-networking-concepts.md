# Task 1: DNS – How Names Become IPs
When google.com is typed it checks corrosponding ip in local catche. If not found it send request to DNS resolver. 
The query goes to root and checks if it exists then check TLD (.com) and finally Authoritative server to locate IP address to initaite a connection on given browser.<br>

### DNS Record Types
*   **`A`**: Maps a human-readable domain name directly to an **IPv4** address.
*   **`AAAA`**: Maps a human-readable domain name directly to an **IPv6** address.
*   **`CNAME`**: Creates an alias that points one domain name to another domain name instead of an IP address.
*   **`MX`**: Specifies the mail server responsible for accepting email messages on behalf of the domain name.
*   **`NS`**: Identifies the authoritative name servers trusted to hold and manage the DNS records for the domain.

<img width="826" height="467" alt="image" src="https://github.com/user-attachments/assets/15fac228-6e6a-41c3-afac-d0fd3e11558e" />

# Task 2: IP Addressing
What is an IPv4 address and how is it structured?
--.--.--.-- consists of 32 bits having 4 decimal can viewed in CIDR address way.
#### 2. Public vs. Private IPs
*   **Public IP**: Globally unique and visible to the entire internet, allowing routers around the world to find your server. 
    *   *Example:* `142.250.190.46` (Google's public web server)
*   **Private IP**: Non-unique, local addresses used exclusively inside a closed local network and completely invisible to the public internet.
    *   *Example:* `192.168.1.25` (A typical home laptop address)

---

#### 3. Private IP Ranges (RFC 1918)
*   **10.x.x.x:** `10.0.0.0` to `10.255.255.255` (Large enterprise networks)
*   **172.16.x.x – 172.31.x.x:** `172.16.0.0` to `172.31.255.255` (Medium cloud/VPC networks)
*   **192.168.x.x:** `192.168.0.0` to `192.168.255.255` (Small home/office networks)

---

#### 4. Identified Private IPs from `ip addr show` Output
Based on the live interface screenshots, this machine utilizes three distinct private IP addresses:
*   **`172.31.43.101` (interface: `ens5`)**: Private Class B IP assigned by AWS VPC for local cloud routing.
*   **`172.17.0.1` (interface: `docker0`)**: Private Class B IP acting as the local virtual bridge gateway for container traffic.
*   **`127.0.0.1` (interface: `lo`)**: Local loopback address reserved exclusively for internal machine self-communication.

# Task 3: CIDR & Subnetting
What does /24 mean in 192.168.1.0/24?
#### 1. Meaning of /24 in 192.168.1.0/24
The `/24` notation (called CIDR notation) indicates that the first **24 bits** of the 32-bit IP address are locked and dedicated to identifying the **network portion**. The remaining 8 bits are left open to be dynamically assigned to individual devices (hosts) living inside that network.

---

#### 2. Usable Hosts Calculation
*   **In a `/24`**: **254 usable hosts** (Calculated as $2^8 - 2$).
*   **In a `/16`**: **65,534 usable hosts** (Calculated as $2^{16} - 2$).
*   **In a `/28`**: **14 usable hosts** (Calculated as $2^4 - 2$).
*   *Note: We always subtract 2 because the very first address is reserved as the Network ID, and the very last address is reserved as the Broadcast address.*

---

#### 3. Why We Subnet
Subnetting means breaking up one single massive network into smaller, isolated, and organized pieces. We do it for three major reasons:
1.  **Security**: It keeps traffic isolated. For example, you can put vulnerable public web servers in one subnet and secure internal financial databases in another subnet, blocking traffic between them.
2.  **Performance**: In a giant network, devices constantly broadcast signals to everyone. Subnetting puts up walls so noisy broadcast traffic stays inside its own small zone instead of slowing down the entire company.
3.  **Efficiency**: It prevents wasting millions of IP addresses by tailoring the network size exactly to the number of devices that need it.

---

#### 4. Quick Exercise Table


| CIDR | Subnet Mask | Total IPs | Usable Hosts |
| :--- | :--- | :--- | :--- |
| **/24** | `255.255.255.0` | 256 | **254** |
| **/16** | `255.255.0.0` | 65,536 | **65,534** |
| **/28** | `255.255.255.240` | 16 | **14** |

# Task 4  Ports – The Doors to Services
### Task 4: Ports – The Doors to Services

#### 1. Definition & Purpose
*   **What it is:** A 16-bit number (0–65535) acting as a specific application doorway inside an OS.
*   **Why we need them:** IP addresses route data to the **machine**; ports route data to the specific **software service**. They allow a single server to run multiple network applications simultaneously (e.g., hosting a website while allowing SSH access).

---

#### 2. Common Ports Reference


| Port | Service | Core Function |
| :--- | :--- | :--- |
| **22** | **SSH** | Secure remote server management. |
| **80** | **HTTP** | Standard, unencrypted web traffic. |
| **443** | **HTTPS** | Secure, encrypted web traffic (SSL/TLS). |
| **53** | **DNS** | Domain name resolution to IP addresses. |
| **3306** | **MySQL** | Relational database connection endpoint. |
| **6379** | **Redis** | Fast, in-memory caching and data store. |
| **27017**| **MongoDB** | NoSQL document database connection endpoint. |

---

#### 3. Live Screen Mapping (`sudo ss -tulpn`)
Two active ports identified and verified directly from the system logs:
*   **Port 80 $\rightarrow$ Nginx (`nginx`)**: The web server software actively waiting on Port 80 to deliver HTTP web content.
*   **Port 22 $\rightarrow$ SSH Daemon (`sshd`)**: The secure shell mechanism holding open Port 22 to maintain this terminal configuration session.

# Task 5: Putting It Together

## 📝 Scenario Analysis & Troubleshooting

### 1. Concepts in `curl http://myapp.com:8080`
* **DNS Resolution:** Translating `myapp.com` to a Layer 3 IP address.
* **TCP Transport:** Opening a reliable connection over custom **Port 8080**.
* **HTTP Application:** Sending an unencrypted web request to fetch application data.

---

### 2. First Checks for Database Failure (`10.0.1.50:3306`)
* **Run `ping 10.0.1.50`:** Confirms if the machine is alive inside the private subnet.
* **Run `nc -zv 10.0.1.50 3306`:** Checks if the MySQL database application is listening or if a firewall is blocking that specific port.
