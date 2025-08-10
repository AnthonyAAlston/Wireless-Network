# ​ Network+ Lab 19 — Secure Wireless LAN Setup (Cisco Packet Tracer)

Set up a secure wireless LAN using a Linksys WRT300N router connected to Router1. You'll configure WAN/LAN IPs, enable DHCP, hide the SSID, secure Wi-Fi, connect a wireless client, and verify connectivity.

---

##  Topology & Addressing

### Topology Diagram
![Topology](s6.png)

| Device             | Interface | IP Address     | Subnet Mask     | Default Gateway |
|--------------------|-----------|----------------|-----------------|-----------------|
| **Router1**        | G0/0      | 152.10.10.10   | 255.255.255.0   | N/A             |
| **PC1 (Wired)**    | NIC       | 152.10.10.20   | 255.255.255.0   | 152.10.10.10    |
| **Wireless Router**| WAN       | 152.10.10.30   | 255.255.255.0   | 152.10.10.10    |
| **Wireless Router**| LAN       | 172.17.20.1    | 255.255.255.0   | N/A             |
| **PC2 (Wireless)** | NIC       | DHCP-assigned  | 255.255.255.0   | 172.17.20.1     |

---

##  Objectives

1. Configure WAN and LAN settings on the wireless router  
2. Enable DHCP for wireless clients  
3. Set up wireless security (WPA2, hidden SSID)  
4. Connect a wireless client manually  
5. Verify internal LAN to LAN connectivity

---

##  Step-by-Step Configuration

### 1. WAN (Internet) Configuration on Wireless Router
- Navigate to **GUI → Setup**  
- Choose **Static IP**, then set:
  - IP: `152.10.10.30`
  - Mask: `255.255.255.0`
  - Gateway: `152.10.10.10`  
- Save  
![WAN Setup](s7.png)

### 2. LAN & DHCP Setup
- Go to **Network Setup**
  - Set router IP: `172.17.20.1`
  - Subnet mask: `255.255.255.0`
  - Enable DHCP: Range `172.17.20.100–149` (max 50 users)  
- Save  

### 3. Wireless Basic Settings
- Access **Wireless → Basic Wireless Settings**
  - Mode: `Wireless-N Only`
  - SSID: `WRT_LAN`
  - Disable SSID Broadcast  
- Save  
![Wireless Basic](s8.png)

### 4. Wireless Security
- Under **Wireless → Wireless Security**
  - Security: `WPA2-Personal`
  - Encryption: `AES`
  - Passphrase: `password123`  
- Save  
![Wireless Security](s9.png)

### 5. PC1 (Wired) Configuration
- On PC1: go to **Desktop → IP Configuration**
  - IP: `152.10.10.20`
  - Mask: `255.255.255.0`
  - Gateway: `152.10.10.10`

### 6. PC2 (Wireless) Configuration—Hidden SSID
- On PC2: **Desktop → PC Wireless → Advanced Setup**
  - Mode: `Infrastructure`
  - SSID: `WRT_LAN`
  - Security: `WPA2-Personal`, Passphrase: `password123`  
- Save profile, connect  
![Connecting](s3.png)
- Check signal/link quality  
![Connected](s4.png)

### 7. Connectivity Verification
- On PC2, open terminal and ping PC1:
  ```bash
  ping 152.10.10.20
