# WLANPi + Wavelify Golden Image

**Enterprise-grade WiFi survey solution with multi-radio scanning and mobile app integration**

![WLANPi + Wavelify](https://wavelify.com/wlanpi)

---

## 🌟 Overview

This golden image transforms your WLANPi R4 into an enterprise-grade WiFi survey device with seamless Wavelify mobile app connectivity. Pre-configured with all necessary services, drivers, and optimizations for professional wireless site surveys.

## ✨ Features

### **Multi-Radio WiFi Scanning**
- ✅ Parallel scanning across multiple WiFi adapters
- ✅ Automatic BSSID deduplication (strongest signal wins)
- ✅ Support for 2.4 GHz, 5 GHz, and 6 GHz bands
- ✅ Real-time WiFi data via REST API
- ✅ Optimized scan timeouts (12 seconds per interface)

### **Mobile Connectivity**
- ✅ **Bluetooth SPP** - Wireless connection for Android devices
- ✅ **USB-C Ethernet** - Wired connection (169.254.42.1)
- ✅ Permanent Bluetooth discoverability
- ✅ Auto-pairing support
- ✅ JSON-over-RFCOMM protocol

### **Auto-Configured Services**
All services start automatically on boot:
- **wlanpi-api.service** - WiFi scan API server (port 8080)
- **wlanpi-spp.service** - Bluetooth SPP server
- **keep-pairable.service** - Maintains Bluetooth pairable state

### **Zero Configuration**
- ✅ No manual setup required
- ✅ All WiFi interfaces auto-detected
- ✅ Services auto-start on boot
- ✅ Permanent Bluetooth discoverability
- ✅ Pre-configured networking

### **Additional Features**
- ✅ GPS geotagging support (via gpsd)
- ✅ REST API on port 8080
- ✅ Systemd service management
- ✅ WiFi power management optimized
- ✅ Multi-radio deduplication

---

## 📋 System Requirements

### **Hardware**
- **Device:** WLANPi R4 (Raspberry Pi CM4-based)
- **SD Card:** 16GB minimum (32GB recommended)
- **WiFi Adapters:** Any supported USB WiFi adapters (multi-radio capability)
- **Power:** USB-C power supply (5V/3A recommended)

### **Compatible WiFi Adapters**
- MediaTek MT7921 (built-in)
- Any Linux-compatible USB WiFi adapters
- Supports 2.4/5/6 GHz bands (adapter-dependent)

### **Mobile Device Requirements**
- **Android:** Bluetooth SPP support required
- **iOS:** Not currently supported (BLE coming soon)
- **Wavelify App:** Available on Android

---

## 🚀 Quick Start Guide

### **Download the Image**

**⬇️ [Download WLANPi + Wavelify Golden Image (799 MB)](https://github.com/wavelify/wlanpi_os_wavelify/releases/latest/download/wlanpi-wavelify.img.xz)**

**Option 1: Direct Download (Recommended)**
```bash
# Download the compressed golden image (799 MB)
wget https://github.com/wavelify/wlanpi_os_wavelify/releases/latest/download/wlanpi-wavelify.img.xz

# Verify checksum (optional but recommended)
sha256sum wlanpi-wavelify.img.xz
```

**Option 2: Using curl**
```bash
curl -L -o wlanpi-wavelify.img.xz \
  https://github.com/wavelify/wlanpi_os_wavelify/releases/latest/download/wlanpi-wavelify.img.xz
```

**Option 3: Clone Repository (Documentation only)**
```bash
git clone https://github.com/wavelify/wlanpi_os_wavelify.git
cd wlanpi_os_wavelify
# Note: The image file is in GitHub Releases, not the git repo
```

### **Flash to SD Card**

#### **Method 1: Balena Etcher (Recommended for beginners)**

1. **Download Balena Etcher**
   - Visit: https://www.balena.io/etcher/
   - Download and install for your OS

2. **Decompress the Image** (if needed)
   ```bash
   xz -d wlanpi-wavelify.img.xz
   ```

3. **Flash with Etcher**
   - Insert SD card into your computer
   - Launch Balena Etcher
   - Select `wlanpi-wavelify.img`
   - Select your SD card drive
   - Click **Flash!**
   - Wait for completion and verification

#### **Method 2: Command Line (macOS/Linux)**

**macOS:**
```bash
# 1. Decompress the image
xz -d wlanpi-wavelify.img.xz

# 2. Find your SD card
diskutil list
# Look for your SD card (e.g., /dev/disk4)

# 3. Unmount the SD card
diskutil unmountDisk /dev/diskN
# Replace N with your disk number

# 4. Flash the image
sudo dd if=wlanpi-wavelify.img of=/dev/rdiskN bs=4m status=progress
# Using rdiskN (with 'r') is faster than diskN

# 5. Eject safely
diskutil eject /dev/diskN
```

**Linux:**
```bash
# 1. Decompress the image
xz -d wlanpi-wavelify.img.xz

# 2. Find your SD card
lsblk
# Look for your SD card (e.g., /dev/sdb)

# 3. Unmount the SD card
sudo umount /dev/sdX*
# Replace X with your device letter

# 4. Flash the image
sudo dd if=wlanpi-wavelify.img of=/dev/sdX bs=4M status=progress conv=fsync

# 5. Sync and eject
sync
sudo eject /dev/sdX
```

#### **Method 3: Windows (Win32 Disk Imager)**

1. Download and install [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/)
2. Decompress `wlanpi-wavelify.img.xz` using [7-Zip](https://www.7-zip.org/)
3. Run Win32 Disk Imager as Administrator
4. Select the `.img` file and your SD card drive
5. Click **Write**

---

## 🔌 First Boot & Setup

### **1. Insert and Boot**
1. Insert the flashed SD card into your WLANPi R4
2. Ensure correct orientation (contacts facing down)
3. Connect USB-C power
4. Wait 30-60 seconds for initial boot
5. LED indicators will show activity

### **2. Connect Your Android Device**

#### **Bluetooth SPP Connection (Wireless)**

**Step 1: Enable Bluetooth**
- On your Android device, go to **Settings** → **Bluetooth**
- Turn Bluetooth **ON**

**Step 2: Scan for WLANPi**
- Make sure WLANPi is powered on
- Scan for new devices
- Look for a device named **wlanpi-***

**Step 3: Pair**
- Tap on the WLANPi device
- Accept any pairing requests
- Device will remain permanently discoverable

**Step 4: Open Wavelify App**
- Launch the Wavelify Android app
- App will auto-detect the paired WLANPi
- Connection via Bluetooth SPP is automatic

**Step 5: Start Surveying**
- Begin your WiFi survey
- Multi-radio scanning is active
- Real-time data from all WiFi adapters

#### **Ethernet Connection (Wired)**

**For initial setup or debugging:**

1. **Connect via USB-C Ethernet Adapter**
   - Use a USB-C to Ethernet adapter
   - Connect between your phone/laptop and WLANPi

2. **Configure Network**
   - The WLANPi uses static IP: **169.254.42.1**
   - Your device should auto-configure via DHCP

3. **Access the API**
   ```bash
   # Test connection
   curl http://169.254.42.1:8080/api/v1/scan

   # Expected response: JSON with WiFi scan data
   ```

4. **API Endpoints**
   - Scan: `http://169.254.42.1:8080/api/v1/scan`
   - Device Info: `http://169.254.42.1:8080/api/v1/device/info`
   - Status: `http://169.254.42.1:8080/api/v1/device/status`

---

## 🔧 Technical Details

### **Services**

All services are managed by systemd and auto-start on boot:

| Service | Description | Port |
|---------|-------------|------|
| `wlanpi-api.service` | WiFi scan API server | 8080 |
| `wlanpi-spp.service` | Bluetooth SPP server | RFCOMM |
| `keep-pairable.service` | Bluetooth pairing manager | - |

**Service Management:**
```bash
# Check service status
sudo systemctl status wlanpi-api
sudo systemctl status wlanpi-spp

# View logs
sudo journalctl -u wlanpi-api -f
sudo journalctl -u wlanpi-spp -f

# Restart services
sudo systemctl restart wlanpi-api
sudo systemctl restart wlanpi-spp
```

### **WiFi Scanning**

**Multi-Radio Implementation:**
- Automatically detects all WiFi interfaces (`wlan*`, `wlp*`)
- Parallel scanning via Python threading
- BSSID deduplication (keeps strongest signal)
- Optimized 12-second timeout per interface

**Scan Method:**
- Uses `iw dev <interface> scan` command
- Parses beacon frames for:
  - SSID, BSSID, Signal (dBm)
  - Frequency, Channel, Band (2.4/5/6 GHz)
  - Security (WPA3/WPA2/WPA/WEP/Open)
  - WiFi standard, Bandwidth

**Data Format (JSON):**
```json
{
  "networks": [
    {
      "ssid": "MyNetwork",
      "bssid": "AA:BB:CC:DD:EE:FF",
      "signal": -45,
      "frequency": 5180,
      "channel": 36,
      "band": "5GHz",
      "security": "WPA2",
      "bandwidth": 80
    }
  ],
  "is_simulated": false,
  "scan_time": 1.234
}
```

### **Bluetooth Configuration**

**SPP (Serial Port Profile):**
- UUID: `00001101-0000-1000-8000-00805F9B34FB`
- Protocol: JSON over RFCOMM
- Device Name: Auto-generated from hostname
- Discoverable Timeout: 0 (permanent)
- Auto-pairing: Enabled

**Configuration File:** `/etc/bluetooth/main.conf`
```ini
[General]
Name = wlanpi-<hostname>
DiscoverableTimeout = 0
AlwaysPairable = true

[Policy]
AutoEnable = true
```

### **Networking**

**Ethernet (eth0):**
- Static IP: 169.254.42.1/24
- No gateway (isolated network)
- No DNS (phone keeps WiFi internet)

**WiFi Interfaces:**
- Managed by `wlanpi-api` service
- Auto-detected at startup
- Power management disabled via udev rules

### **File Locations**

| Path | Description |
|------|-------------|
| `/opt/wlanpi/` | Application files |
| `/etc/systemd/system/wlanpi-*.service` | Service definitions |
| `/etc/bluetooth/main.conf` | Bluetooth configuration |
| `/etc/udev/rules.d/99-wifi-power.rules` | WiFi power management |

---

## 🐛 Troubleshooting

### **Services Won't Start**

```bash
# Check service status
sudo systemctl status wlanpi-api
sudo systemctl status wlanpi-spp

# View detailed logs
sudo journalctl -u wlanpi-api -n 50
sudo journalctl -u wlanpi-spp -n 50

# Restart services
sudo systemctl restart wlanpi-api
sudo systemctl restart wlanpi-spp

# Reload systemd if you made changes
sudo systemctl daemon-reload
```

### **Bluetooth Not Discoverable**

```bash
# Check Bluetooth status
sudo systemctl status bluetooth

# Make discoverable manually
echo -e "power on\ndiscoverable on\ndiscoverable-timeout 0\npairable on\nquit" | bluetoothctl

# Check if keep-pairable service is running
sudo systemctl status keep-pairable
```

### **WiFi Scan Returns Empty**

```bash
# Check if WiFi interfaces are up
ip link show | grep wlan

# Bring up interfaces manually
sudo ip link set wlan0 up
sudo ip link set wlan1 up

# Test scan manually
sudo iw dev wlan0 scan

# Check service logs
sudo journalctl -u wlanpi-api -f
```

### **Can't Connect via Ethernet**

```bash
# Check if eth0 is configured
ip addr show eth0

# Should show: 169.254.42.1/24

# Test API directly on WLANPi
curl http://localhost:8080/api/v1/scan
```

### **Reset to Factory Settings**

```bash
# Re-flash the SD card with the golden image
# All customizations will be lost
```

---

## 📊 Performance

### **Scan Performance**
- **Single Radio:** ~3-5 seconds per scan
- **Dual Radio:** ~3-5 seconds (parallel)
- **Triple Radio:** ~3-5 seconds (parallel)
- **Network Detection:** 20-100+ networks per scan

### **Resource Usage**
- **RAM:** ~200-300 MB (idle)
- **CPU:** 10-20% (active scanning)
- **Disk:** ~2.5 GB (OS + services)

---

## 🔐 Security Notes

### **Default Configuration**
- ⚠️ No password authentication on API
- ⚠️ Bluetooth always discoverable
- ⚠️ Designed for isolated field use
- ⚠️ Not intended for public networks

### **Production Recommendations**
- Use in isolated networks only
- Do not expose to internet
- Keep Bluetooth range limited
- Update regularly for security patches

---

## 📦 Image Details

| Property | Value |
|----------|-------|
| **Base OS** | Raspberry Pi OS (Debian 12 Bookworm) |
| **Kernel** | Linux 6.1+ |
| **Python** | 3.9+ |
| **Image Size (Uncompressed)** | ~29.7 GB |
| **Image Size (Compressed)** | ~799 MB (.xz) |
| **Minimum SD Card** | 16 GB |
| **Recommended SD Card** | 32 GB |
| **Architecture** | ARM64 (aarch64) |

---

## 🛠️ Build Information

### **Pre-installed Packages**
- Python 3.9+
- FastAPI + Uvicorn
- BlueZ (Bluetooth stack)
- wireless-tools / iw
- gpsd (GPS support)
- systemd services

### **Custom Components**
- Multi-radio WiFi scanner
- Bluetooth SPP server
- REST API server
- Auto-configuration scripts

---

## 📝 Version History

### **v1.0** (Current)
- Initial golden image release
- Multi-radio WiFi scanning
- Bluetooth SPP support
- Auto-configured services
- Wavelify mobile app integration

---

## 🤝 Support

### **Issues & Bugs**
Report issues on GitHub: [Issues Page](https://github.com/YOUR_REPO/issues)

### **Documentation**
Visit: [wavelify.com/wlanpi](https://wavelify.com/wlanpi)

### **Contact**
- Email: support@wavelify.com
- Website: https://wavelify.com

---

## 📄 License

This golden image is provided for use with Wavelify services.

**Included Open Source Components:**
- Raspberry Pi OS: [License](https://www.raspberrypi.com/software/)
- Python packages: Various open source licenses
- BlueZ: GPLv2

---

## 🙏 Acknowledgments

- WLANPi Project - https://wlanpi.com
- Raspberry Pi Foundation
- Wavelify Team

---

## 🚀 Quick Reference Card

```bash
# Flash SD card
xz -d wlanpi-wavelify.img.xz
sudo dd if=wlanpi-wavelify.img of=/dev/rdiskN bs=4m

# First boot
1. Insert SD card
2. Power on
3. Wait 60 seconds

# Connect (Android)
1. Enable Bluetooth
2. Scan for "wlanpi-*"
3. Pair device
4. Open Wavelify app

# Connect (Ethernet)
IP: 169.254.42.1
API: http://169.254.42.1:8080/api/v1/scan

# Service management
sudo systemctl status wlanpi-api
sudo systemctl restart wlanpi-spp
sudo journalctl -u wlanpi-api -f
```

---

**Made with ❤️ by [Wavelify](https://wavelify.com)**
