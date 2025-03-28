# WireGuard + Proton VPN Setup on Cudy Router

![REQUIRED](https://img.shields.io/badge/SUPPORTED-Cudy_WR2100_Series-blue)

<p align="center">
  <img src="https://ptpimg.me/r0516m.png" alt="Cudy Router + Proton VPN" style="width: 10%;">
</p>

_This guide will walk you through configuring Proton VPN via WireGuard protocol on your Cudy router to encrypt all network traffic._

---

<div style="border: 2px solid #2ecc71; background-color: #e8f8f5; padding: 10px; border-radius: 5px; margin: 15px 0;">
  <strong>ℹ️ Requirements:</strong>
  <ul>
    <li>Cudy router with latest firmware</li>
    <li>Active Proton VPN subscription</li>
    <li>WireGuard configuration file from Proton VPN</li>
  </ul>
</div>

---

Common network topology:

<p align="center">
  <img src="https://i.ibb.co/LjkDgfy/image.png" alt="Cudy Router" style="width: 50%;">
</p>

## Configuration Steps

### 1. Access Router Interface

1. Connect to your Cudy network.
2. Open [http://yourrouteradress](http://yourrouteradress) in your browser.
3. Enter your credentials.

### 2. Navigate to VPN Section

- Go to **General Settings** → **VPN** → **WireGuard VPN**.

<p align="center">
  <img src="https://i.ibb.co/G4wVXtST/image.png" alt="config-router-cudy" style="width: 60%;">
</p>

### 3. Import Proton VPN Configuration

1. **Obtain the WireGuard Configuration:**
   - Login to your Proton VPN account.
   - Navigate to **Downloads** → **WireGuard Configuration**.
   - Select **Router** as the device type.
   - Choose your desired server and download the `.conf` file.

<p align="center">
  <img src="https://i.ibb.co/wNQRdzLr/image.png" alt="Proton VPN" style="width: 60%;">
</p>

2. **Upload the Configuration to Your Router:**
   - Click on **[Browse]** and select the downloaded `.conf` file.
   - Click **Import** to load the configuration.
  
<p align="center">
  <img src="https://i.ibb.co/bjnPp5QP/image.png" alt="config-router-WireGuard" style="width: 60%;">
</p>

<div style="border: 2px solid #f39c12; background-color: #fef5e7; padding: 10px; border-radius: 5px; margin: 15px 0;">
  <strong>⚠️ Important:</strong> Enable the "VPN Kill Switch" under VPN Policy settings to prevent IP leaks!
</div>

### 4. Advanced Settings

- **VPN Policy Options:**
  - **Kill Switch:** Enabled
  - **Domain Bypass:** Add local domains as needed
  - **Remote Subnets:** 10.2.0.0/24

- **Device-Specific Rules:**
  - Navigate to **System Status** → **Devices** → Select the device → Toggle VPN on/off

<p align="center">
  <img src="https://i.ibb.co/Kj8b36Wn/image.png" alt="config-router-Devices" style="width: 60%;">
</p>

---

## Verification Commands

```bash
# Check VPN connection status
ping 10.2.0.1

# Test DNS leaks
nslookup protonvpn.com

# Verify public IP
curl ifconfig.io
```

<div style="border: 2px solid #e74c3c; background-color: #f9e6e6; padding: 10px; border-radius: 5px; margin: 15px 0;">
  <strong>🚨 Troubleshooting:</strong> If the connection fails, verify:
  <ul>
    <li>WireGuard port 51820 is open</li>
    <li>The router’s time/date settings are correct</li>
    <li>Your Proton VPN credentials are valid</li>
  </ul>
</div>

---

## Configuration File Example

```conf
[Interface]
PrivateKey = ABC123...
Address = 10.2.0.2/32
DNS = 10.8.8.1

[Peer]
PublicKey = XYZ789...
AllowedIPs = 0.0.0.0/0
Endpoint = us-free-123.protonvpn.net:51820
```

---

## FAQ

**Q: Can I use free Proton VPN accounts?**  
A: WireGuard requires a Proton VPN Plus or higher subscription.

**Q: How do I update the configurations?**  
A: Re-generate the configuration monthly from the Proton VPN dashboard and re-import it.

**Q: What about local network access?**  
A: Add your local subnets (e.g., 192.168.x.x) to the Domain Bypass list.

---

<div style="border: 2px solid #3498db; background-color: #ebf5fb; padding: 10px; border-radius: 5px; margin: 15px 0;">
  <strong>🔒 Security Best Practices:</strong>
  <ul>
    <li>Rotate WireGuard keys quarterly</li>
    <li>Enable router auto-updates</li>
    <li>Utilize Proton VPN Secure Core servers</li>
  </ul>
</div>
