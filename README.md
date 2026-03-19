# ESP32-EvilTwin

ESP32-EvilTwin: Dual-Radio Security Awareness Hub


01 - Project Overview


This project is a sophisticated hardware-software demonstration designed to showcase the inherent security vulnerabilities of the 2.4GHz Wi-Fi spectrum. By simulating a Captive Portal / Evil Twin attack scenario in a controlled, isolated environment, it aims to educate users on the risks of connecting to untrusted networks. The system utilizes an ESP32-U with a dual nRF24L01 radio setup and an OLED display to provide a real-time monitor of the attack and verification process.


02 - Key Features


Dual-Radio Architecture: Uses both HSPI and VSPI buses to manage two nRF24L01 modules for out-of-band data monitoring.

Dynamic Management Portal: Starts an initial DEV AP for scanning and target selection via a web interface.

Active Password Verification: Authenticates captured passwords against the actual target router in real-time.

OLED Hardware Monitoring: Real-time display of attack status and captured credentials on the device.

Stealth Exfiltration: Sends verified passwords over nRF24 frequencies to avoid detection on the target network.


03 - Hardware Configuration (Pinout)


Since the source code is private, please follow this specific wiring diagram to ensure compatibility with the ESP32-EvilTwin.bin firmware:

Component	     Pin Function	       ESP32 Pin
OLED Display	   SDA	             GPIO 4
OLED Display	   SCL	             GPIO 5
nRF24L01 (HSPI) 	CE / CSN	       GPIO 16 / 15
nRF24L01 (HSPI)	SCK / MISO / MOSI	 GPIO 14 / 12 / 13
nRF24L01 (VSPI)	CE / CSN           GPIO 22 / 21
nRF24L01 (VSPI)	SCK / MISO / MOSI	 GPIO 18 / 19 / 23

Note: Use 10µF decoupling capacitors between VCC and GND for each nRF24L01 module to ensure power stability.


04 - Installation (Flashing the Firmware)


To install the system on your ESP32-U:

Download: Get the ESP32-EvilTwin.bin file from this repository.

Tool: Use the ESP Web Tools or Flash Download Tool by Espressif.

Settings: * Flash Address: 0x10000

Baudrate: 115200

Action: Connect your ESP32 via USB, select the COM port, and flash the binary file.


05 - The Workflow


Admin Setup: Boot the device to create the DEV Wi-Fi AP (Password: 12345678).

Target Selection: Access 192.168.4.1 in your browser, scan, and select your target network.

The Simulation: The device clones the target SSID and serves a professional "Firmware Update" page.

Verification: * Success: Verified passwords appear on the OLED and are sent via nRF24.

Failure: User is prompted to retry on the phishing page.


06 - Ethical & Educational Disclaimer


This project is for EDUCATIONAL PURPOSES ONLY.

Designed to demonstrate 2.4GHz insecurity and promote 5GHz/WPA3 adoption.

Never use this tool on networks without explicit permission.

The author is not responsible for any misuse or damage.
