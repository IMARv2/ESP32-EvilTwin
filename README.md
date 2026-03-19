# 🛡️ ESP32-EvilTwin: Dual-Radio Security Awareness Hub

> [!IMPORTANT]
> **PURPOSE:** A specialized hardware-software demonstration platform designed to audit and showcase 2.4GHz Wi-Fi vulnerabilities.

---

## 01 - Project Overview

> [!NOTE]
> **Vulnerability Demonstration:** This project is a sophisticated hardware-software demonstration designed to showcase the inherent security vulnerabilities of the 2.4GHz Wi-Fi spectrum. 

By simulating a **Captive Portal / Evil Twin** attack scenario in a controlled, isolated environment, it aims to educate users on the risks of connecting to untrusted networks. The system utilizes an **ESP32-U** with a **dual nRF24L01 radio setup** and an **OLED display** to provide a real-time monitor of the attack and verification process.

---

## 02 - Key Features

* **Dual-Radio Architecture:** Orchestrates both **HSPI** and **VSPI** buses to manage dual nRF24L01 modules for out-of-band data monitoring.
* **Dynamic Management Portal:** Initializes a standalone `DEV` Access Point for environment scanning and target acquisition via a web-based GUI.
* **Active Credential Verification:** Performs **Real-Time Authentication** against the target AP to confirm password validity.
* **OLED Telemetry:** Provides a localized hardware readout of system status, target locking, and captured clear-text credentials.
* **Stealth Exfiltration:** Forwards verified credentials over non-Wi-Fi frequencies (nRF24) to maintain a low profile.

---

## 03 - Hardware Configuration (Pinout)

> [!IMPORTANT]
> **RESTRICTED ACCESS:** The source code for this firmware is proprietary and is not available in this repository. To ensure full compatibility with the pre-compiled `ESP32-EvilTwin.bin` and to avoid I/O conflict, you **MUST** adhere strictly to the following GPIO mapping.

| Component | Pin Function | ESP32 Pin |
| :--- | :--- | :--- |
| **OLED Display** | SDA | **GPIO 4** |
| **OLED Display** | SCL | **GPIO 5** |
| **nRF24L01 (HSPI)** | CE / CSN | **GPIO 16 / 15** |
| **nRF24L01 (HSPI)** | SCK / MISO / MOSI | **GPIO 14 / 12 / 13** |
| **nRF24L01 (VSPI)** | CE / CSN | **GPIO 22 / 21** |
| **nRF24L01 (VSPI)** | SCK / MISO / MOSI | **GPIO 18 / 19 / 23** |

> [!TIP]
> **Power Integrity:** Deploy **10µF decoupling capacitors** between VCC and GND for each nRF24L01 module to ensure power stability during high-current operations.

---

## 04 - Installation (Flashing the Firmware)

> [!CAUTION]
> **FIRMWARE SOURCE: INTERNAL USE ONLY. Pre-compiled binaries are provided for deployment.**

1. **Download:** Obtain the latest `ESP32-EvilTwin.bin` from the [Official Releases Section](https://github.com/IMARv2/ESP32-EvilTwin/releases/download/V1.0.0/ESP32-EvilTwin.bin).
2. **Flash Tool:** Utilize [ESP Web Tools](https://web.espressif.com/adash/) or the **Espressif Flash Download Tool**.
3. **Memory Map:** * **Binary Offset:** `0x10000`
    * **SPI Mode:** `DIO`
    * **Flash Freq:** `40MHz`
4. **Execution:** Connect the ESP32-U via USB, initialize the COM port, and execute the 'Flash' command.

---

## 05 - Operational Workflow

> [!NOTE]
> **Sequence of Operations:** Follow these steps to initiate the security demonstration.

1. **Admin Setup:** Boot the device to create the `DEV` Wi-Fi AP (Default Password: `12345678`).
2. **Target Selection:** Access `192.168.4.1` in your browser, perform a scan, and select your target network.
3. **The Simulation:** The device clones the target SSID and serves a professional-grade "Firmware Update" page.
4. **Verification Engine:** * **Success:** Verified passwords appear on the OLED and are exfiltrated via nRF24.
    * **Failure:** User is prompted to retry on the phishing portal if authentication fails.

---

## 06 - Ethical & Educational Disclaimer

> [!WARNING]
> **FOR EDUCATIONAL PURPOSES ONLY.**

* This project is designed to demonstrate 2.4GHz insecurity and promote the adoption of 5GHz/WPA3 standards.
* **PROHIBITED USE:** Never deploy this tool on networks without explicit, written permission from the owner.
* The author assumes **zero liability** for misuse, illegal activities, or hardware damage resulting from this software.
