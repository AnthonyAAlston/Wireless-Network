# 🛜 Network+ Learning Activity #19 — Secure Wireless LAN (Cisco Packet Tracer)

Set up a small secure WLAN using a Linksys WRT300N. You’ll configure WAN/LAN addressing, enable DHCP, secure Wi-Fi with WPA2-Personal, hide the SSID, connect a wireless client manually, and verify connectivity.

---

## 🧭 Topology & Addressing

### Topology
![Topology](s1.png)

### Addressing Table
| Device               | Interface | IP Address     | Subnet Mask     | Default Gateway |
|---------------------|----------:|----------------|-----------------|-----------------|
| **Router1**         | G0/0      | 152.10.10.10   | 255.255.255.0   | —               |
| **PC1 (wired)**     | NIC       | 152.10.10.20   | 255.255.255.0   | 152.10.10.10    |
| **Wireless Router** | WAN       | 152.10.10.30   | 255.255.255.0   | 152.10.10.10    |
| **Wireless Router** | LAN       | 172.17.20.1    | 255.255.255.0   | —               |
| **PC2 (wireless)**  | Wi-Fi     | DHCP assigned  | 255.255.255.0   | 172.17.20.1     |

---

## 🎯 Objectives
- Configure WAN and LAN on the wireless router  
- Enable DHCP for the WLAN  
- Set up Wi-Fi: SSID **WRT_LAN**, **SSID Broadcast: Disabled**, **WPA2-Personal (AES)**  
- Manually join a wireless client to the hidden SSID  
- Verify PC2 → PC1 connectivity

---

## 🛠️ Part 1 — Wireless Router Configuration

### 1) WAN (Internet) Settings
- **GUI → Setup**
- **Internet Connection Type:** Static IP  
  - IP `152.10.10.30`  
  - Mask `255.255.255.0`  
  - Default Gateway `152.10.10.10`
- Save.
  
![WAN Setup](s2.png)

### 2) LAN & DHCP
- **Network Setup**
  - **Router IP:** `172.17.20.1`
  - **Subnet Mask:** `255.255.255.0`
  - **DHCP Server:** Enabled  
    - Start IP `172.17.20.100`  
    - Max Users `50`
- Save.

*(Values match the lab spec.)*

### 3) Basic Wireless Settings
- **Wireless → Basic Wireless Settings**
  - **Network Mode:** Wireless-N Only
  - **SSID:** `WRT_LAN`
  - **SSID Broadcast:** **Disabled**
- Save.

![Basic Wireless Settings](s3.png)

### 4) Wireless Security
- **Wireless → Wireless Security**
  - **Security Mode:** WPA2-Personal
  - **Encryption:** AES
  - **Passphrase:** `password123`
- Save.

![Wireless Security](s4.png)

---

## 🖥️ Part 2 — PC1 (Wired Host)

- **PC1 → Desktop → IP Configuration**
  - IP `152.10.10.20`
  - Mask `255.255.255.0`
  - Gateway `152.10.10.10`

---

## 📶 Part 3 — PC2 (Wireless Client, Hidden SSID)

Because SSID broadcast is disabled, create a manual profile.

1) **PC2 → Desktop → PC Wireless**  
   On **Available Wireless Networks**, click **Advanced Setup**.
   ![Available Networks / Advanced Setup](s5.png)

2) **Creating a Profile**
   - **Wireless Mode:** Infrastructure  
   - **Wireless Network Name (SSID):** `WRT_LAN`  
   - Next.
   ![Enter SSID (Infrastructure Mode)](s6.png)

3) **Security**
   - **WPA2-Personal** → Next  
   - Passphrase: `password123` → Next
   ![Choose WPA2-Personal](s7.png)

4) **Confirm & Save**
   - Review profile → **Save** → **Connect to Network**
   ![Confirm New Settings](s8.png)

5) **Connected Status**
   - Verify **Signal Strength** and **Link Quality** are green.
   ![Connected / Link Quality](s9.png)

---

## 🔍 Part 4 — Verify Connectivity (Inside → Outside)

On **PC2** open **Command Prompt** and ping **PC1**:

```bash
ping 152.10.10.20
