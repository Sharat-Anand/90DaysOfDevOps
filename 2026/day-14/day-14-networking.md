# OSI Model(Open Systems Interconnection)
7. APPLICATION   [Data]      -> Human-computer interaction (HTTP, SMTP, DNS)
6. PRESENTATION  [Data]      -> Encryption, compression, syntax (SSL/TLS, JPEG)
5. SESSION       [Data]      -> Manages connections & dialogs (NetBIOS, RPC)
4. TRANSPORT     [Segments]  -> End-to-end delivery & flow control (TCP 3 way handshak, UDP 2 way handshake)
3. NETWORK       [Packets]   -> Routing & IP addressing (IPv4, IPv6, Routers)
2. DATA LINK     [Frames]    -> Physical addressing & switching (MAC, Switches)
1. PHYSICAL      [Bits]      -> Cables, voltage, and raw signals (Ethernet, Fiber)

# Transmission Control Protocol/Internet Protocol
4. APPLICATION    [Data]      -> Apps, services, and formatting (HTTP, DNS, SSH)
3. TRANSPORT      [Segments]  -> Host-to-host delivery & flow control (TCP, UDP)
2. INTERNET       [Packets]   -> Routing, logical addressing (IPv4, IPv6, ICMP)
1. NETWORK ACCESS [Frames/Bits]-> Physical hardware and local link (Ethernet, Wi-Fi)

# Example
Curl https://...../

[curl] ──> is an HTTP Request ──> over a TCP Segment ──> inside an IP Packet ──> over an Ethernet Frame
            (Application)            (Transport)             (Internet)         (Network Access)

4. APPLICATION    [Data]      -> curl, curl -I, dig, nslookup
3. TRANSPORT      [Segments]  -> ss, netstat
2. INTERNET       [Packets]   -> ping, traceroute
1. NETWORK ACCESS [Frames]    -> ip addr show
            
---

## 🛠️ Layer-by-Layer Command Map (1-Liners)

### Layer 4: Application Layer
*   **`curl <url>`**
    *   **Why it is used:** To request and download the full source code, files, or API data payloads from a web server.
*   **`curl -I <url>`**
    *   **Why it is used:** To grab *only* the HTTP metadata headers to quickly check website status codes (e.g., 200, 403, 404) and server security.
*   **`dig <domain>`**
    *   **Why it is used:** To query DNS servers on UDP Port 53 and retrieve highly detailed technical records (A, MX, TXT) for a domain.
*   **`nslookup <domain>`**
    *   **Why it is used:** To perform a simple, universal DNS lookup to quickly verify the raw IP address assigned to a human domain name.

### Layer 3: Transport Layer
*   **`ss -tulpn`**
    *   **Why it is used:** To look inside the local OS and see exactly which application names and Process IDs (PIDs) are listening on which TCP/UDP ports.
*   **`netstat -an | head`**
    *   **Why it is used:** To look inside legacy systems and preview the first 10 rows of active socket connections and port mappings.

### Layer 2: Internet Layer
*   **`ping <ip/domain>`**
    *   **Why it is used:** To send lightweight ICMP signals to check if a remote server is alive and measure connection latency in milliseconds.
*   **`traceroute <domain>`**
    *   **Why it is used:** To map out the exact geographical path and pinpoint the response times of every single intermediate router hop to a destination.

### Layer 1: Network Access Layer
*   **`ip addr show`**
    *   **Why it is used:** To inspect local network hardware interfaces, look up physical MAC addresses, and verify if a network connection is active (UP/DOWN).

---

## 📋 Quick Blueprint Summary

```text
[Hardware Info]      --> Layer 1 (Network Access) --> ip addr show
[Network Routing]    --> Layer 2 (Internet)       --> ping, traceroute
[OS Ports & Sockets] --> Layer 3 (Transport)      --> ss, netstat
[App Code & Data]    --> Layer 4 (Application)    --> curl, dig, nslookup
```

# Hands-on Checklist
hostname -I ---Only the active IP addresses. A quick check to copy/paste your IP address.<br>
ip addr showIPs  ---MAC addresses, connection status, MTU, and interface names. Deep network troubleshooting and checking physical link layer stats.<br>
ping -c 4 google.com --ping cmd test whether a specific network destination is online and reachable<br>
<img width="1092" height="231" alt="image" src="https://github.com/user-attachments/assets/fa653df2-0771-49e4-8ea2-348b3baed812" />

traceroute google.com ---is used for network path visibility and pinpoint troubleshooting. acts like a GPS roadmap that tells you exactly where the breakdown is happening<br>
<img width="1452" height="232" alt="image" src="https://github.com/user-attachments/assets/86e388fd-62b2-487c-bf90-cfaf842e98c7" />

sudo ss -tulpn --- Linux utility used to display active network sockets.<br> 
Port Conflict Troubleshooting: If you try to launch a web server and it crashes saying "Port 80 already in use", running ss -tulpn will instantly reveal the exact process name and ID blocking that port.<br>
<img width="1400" height="227" alt="image" src="https://github.com/user-attachments/assets/b74f47a5-b8d4-4413-bd96-f2f76cce3df7" />

nslookup google.com --A legacy, simple tool for a quick, straightforward IP verification.
[dig / nslookup] ──> Application Layer tools using UDP Port 53 to convert human domain names to Layer 3 IP addresses.
<img width="562" height="210" alt="image" src="https://github.com/user-attachments/assets/76d23488-5c37-4e1b-92c5-d9c83647df97" />

dig google.com ---The modern highly detailed, showing exact server transaction times, response headers, and structured raw data.<br>
<img width="831" height="467" alt="image" src="https://github.com/user-attachments/assets/7d07b74c-b4b6-4277-831e-d2fc24da0130" />

 curl -I google.com --Troubleshooting HTTP status codes: Instantly verify if a site returns 200 OK, 301 Redirect, 403 Forbidden, or 500 Server Error.<br>
 Analyzing Security & Server Software (Footprinting)<br>
  Verifying Cache and Content Types - It tells you what kind of file is sitting at the URL via the content-type <br>
<img width="1451" height="327" alt="image" src="https://github.com/user-attachments/assets/b0ac0eb7-7cbd-405c-bfb3-bf096e2bbed9" />

netstat -an | head --(new is ss tulpn)troubleshooting pipeline used to check the very first few lines of your system's active network connections.<br>
<img width="912" height="276" alt="image" src="https://github.com/user-attachments/assets/7e0a6865-8e58-480f-bf60-8feff82896c0" />
