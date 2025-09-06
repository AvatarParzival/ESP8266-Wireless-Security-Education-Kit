# Wi-Fi 802.11 Deauth Lab (ESP8266)

**Description:**  
Educational firmware for the **ESP8266 NodeMCU** that demonstrates Wi-Fi deauthentication in a **controlled lab setting**. Built for learning about 802.11 protocols, IoT security, and microcontrollers, it highlights why modern defenses like **WPA3, Wi-Fi 6, and Protected Management Frames** are essential.

---

<p align="center">
  <img src="https://i.ibb.co/nMZFsSwf/funq3z3s.png" width="400"/>
</p>

---

## ⚠️ Disclaimer
This project is for **academic and educational purposes only**.  
The firmware must only be used in a **lab environment** on networks and devices you **own or are explicitly authorized to test**.  
Unauthorized use against third-party networks is **illegal and unethical**.  

---

## 📂 Repository Contents
- **`esp8266_deauther.bin`** — Prebuilt firmware image for the ESP8266/NodeMCU board.  

---

## 🧠 About This Firmware
This firmware enables controlled demonstrations of **Wi-Fi management frame behavior** using the ESP8266 NodeMCU.  
It is a hands-on way to study **wireless protocols, embedded hardware, and network vulnerabilities**.

The main feature is the **deauthentication test**, which shows how devices can be disconnected from their network.  
While the concept is old, many low-cost IoT devices remain vulnerable. Modern protections like **Wi-Fi 6** and **Protected Management Frames (802.11w)** mitigate this risk.

With this firmware in a **lab-only environment**, you can:
- Test your own **2.4GHz Wi-Fi networks** to see if they are affected  
- Observe weaknesses in outdated or cheap hardware  
- Understand the importance of **WPA3 and modern equipment**  

---

## 🛠 Requirements
- ESP8266 NodeMCU (with CP2102/CP210x USB-to-UART chip)  
- Micro-USB cable  
- Computer with USB port  
- [CP210x USB Drivers](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers)  
- Python 3.7+ with [`esptool.py`](https://github.com/espressif/esptool)  

> ✅ **Note:** Arduino IDE is **not required**. This project uses **direct binary flashing** via `esptool`.

---

## 🔹 Step 1: Install CP210x Drivers
1. Download drivers from [Silicon Labs](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers).  
2. Install for your OS:  
   - **Windows** → shows up as `COMx` in Device Manager  
   - **Linux/macOS** → `/dev/ttyUSB0` or `/dev/tty.SLAB_USBtoUART`  

---

## 🔹 Step 2: Install esptool
```bash
pip install esptool
```

Verify installation:
```bash
esptool.py version
```

---

## 🔹 Step 3: Connect ESP8266 in Flash Mode
1. Hold down the **FLASH** button on NodeMCU  
2. Press and release **RESET (RST)**  
3. Release **FLASH** → board enters bootloader mode  

---

## 🔹 Step 4: Erase Existing Firmware
Replace `COM3` (Windows) or `/dev/ttyUSB0` (Linux/macOS) with your port:

```bash
esptool.py --port COM3 erase_flash
```

---

## 🔹 Step 5: Flash the Provided Firmware
```bash
esptool.py --port COM3 write_flash -fm dout 0x00000 esp8266_deauther.bin
```

---

## 🔹 Step 6: Reboot & Verify
- Press **RESET** on the NodeMCU  
- The board should reboot and run the firmware  
- Some versions may broadcast a Wi-Fi AP (for lab analysis only)  

---

## 🔐 Accessing the Management Portal (Lab Only)

### Default Access (first boot)
- **SSID (Wi-Fi name):** `pwned`  
- **Password:** `deauther`  
- **Web portal (gateway IP):** `192.168.4.1`  

> ⚠️ These defaults are public knowledge. Do not keep them for lab work — change them immediately.

### Changing Credentials (required for lab use)
1. **Power on the NodeMCU** → it will broadcast the default AP (`pwned`).  
2. **Connect your laptop/phone** using the password `deauther`.  
3. **Open a browser** → go to [http://192.168.4.1](http://192.168.4.1).  
4. In the portal, go to **Settings → AP Settings**.  
5. **Change the SSID** to something lab-specific (e.g., `Lab-ESP8266`).  
6. **Set a strong password** (12–16 characters).  
7. **Save & reboot** → the ESP8266 will now broadcast with your new SSID and password.  
8. Keep the device **isolated/offline** during labs. Power it down when not in use.  

> ✅ Always set your own credentials before running demonstrations. Never expose the default `pwned/deauther` AP in a public environment.

---

## 📜 License & Ethics
- Distributed under the [MIT License](LICENSE) with an **educational use clause**.  
- You are responsible for lawful and ethical use.  
- Do not test on networks/devices you don’t own.  
