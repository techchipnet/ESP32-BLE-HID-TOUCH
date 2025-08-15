<div align="center">

# ESP32 BLE Ducky HID GUI

### A fully customizable, touch-based BLE-Ducky powered by an ESP32.

![Platform](https://img.shields.io/badge/Platform-ESP32-blue.svg)
![Framework](https://img.shields.io/badge/Framework-Arduino-00979D.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)


<img src="https://github.com/user-attachments/assets/f5a33511-e1be-43ed-88ce-8162c68a4e23" alt="ESP32BLEHID" width="300" height="400"/>
</div>

This project transforms an ESP32 and a touchscreen display into a powerful, bluetooth rubber ducky. It connects to your device like pc,laptop or smartphone via Bluetooth LE and acts as a bluetooth keyboard, allowing you to execute complex keystrokes, payloads, macros, and scripts with a single touch.

## ✨ Features

* **Touch-based Interface:** Three fully customizable on-screen buttons.
* **Bluetooth LE Connectivity:** No wires needed; connect directly to your Windows, macOS, Linux computers or Android, iOS Smart phone.
* **Powerful Scripting Engine:** Create complex payloads and scripts via the `payload.txt` file. Supports key combinations, text typing, and delays.
* **External Configuration:** No need to recompile the code to change keystrokes. Simply edit and upload a text file.
* **On-screen Status:** Displays Bluetooth connection status and other information on the screen.
* **Pre-compiled Binary:** No need to compile the sketch. Pre-compiled binary is available in the release page.
* **Ducky Script Compatible:** Easily change & write payloads in Ducky Script style with all keys mapped as in Ducky Script.
* **Web Flasher Support:** Flash your ESP32 directly from your browser using the web flasher at [esptool.spacehuhn.com](http://esptool.spacehuhn.com).

---

## 🛠️ Requirements

### Hardware

1.  **ESP32 WROOM-32U** or any ESP32 development board.
2.  **ILI9341 TFT Touch Display (240x320)** with an XPT2046 touch controller.
3.  **Breadboard and Jumper Wires** for connections.
4.  **Micro-USB Cable** for programming and power.

### Software

1.  **Arduino IDE**. [Arduino](https://www.arduino.cc/en/software/)

---

## 🔌 Connection table

### Display Connections

   | ILI9341 | ESP32        |           
| :------ | :---------------- |
| `VCC` | `3.3V`     |
| `GND` | `GND`     |
| `CS` | `D17`     |
| `RESET` | `D5`     |
| `DC` | `D16`     |
| `SDI(MOSI)` | `D23`     |
| `SCK` | `D18`     |
| `LED` | `D32`     |
| `SDO(MISO)` | `D19`     |

### Touch Connections

  | ILI9341 | ESP32        |           
| :------ | :---------------- |
| `T_CLK` | `D18`     |
| `T_CS` | `D21`     |
| `T_DIN` | `D23`     |
| `T_DO` | `D19`     |
| `T_IRQ` | `-1`     |

---

## ⚙️ Setup and Installation

### Pre-compiled Binary (No Arduino IDE needed)

1. Download the pre-compiled binary from the [Releases](https://github.com/techchipnet/ESP32-BLE-HID-GUI/releases) page.
2. Use one of the following methods to flash the binary:

   #### Web Flasher (Easiest Method)
   1. First install USB to UART Bridge VCP Driver. you can download this driver from here [Driver](https://www.silabs.com/software-and-tools/usb-to-uart-bridge-vcp-drivers?tab=downloads)
   2. Visit [esptool.spacehuhn.com](http://esptool.spacehuhn.com)
   3. Plug in your ESP32 & select the port
   4. Click on "Connect"
   5. Add the downloaded .bin file & set the address
   6. Click "Program" to flash it

   #### Command Line Example
   ```bash
   esptool.py --chip esp32 --port [PORT] --baud 921600 write_flash 0x0 firmware.bin
   ```

### Upload the Payload File (`payload.bin`)

1.  Frist prepare the payload.txt file with your payload, Open termial run the following command to create the `payload.bin` image:
    ```bash
    mkspiffs -c data -b 4096 -p 256 -s 0x160000 payload.bin
    ```
2.  Put the ESP32 into upload mode again.
3.  Now, upload this image to the correct address:
    ```bash
    esptool --chip esp32 --port /dev/cu.usbserial-0001 --baud 921600 write_flash 0x290000 payload.bin
    ```
4.  Restart the ESP32. Your device is now ready!

---

## 🚀 Payload Configuration (Ducky Script Syntax)

You can write your payload in the `payload.txt` file using a simple scripting language.

* **Commands:** `PRESS`, `TYPE`, `DELAY`, `ENTER`
* **Separator:** Separate each command with a semicolon (`;`).

| Command | Example           | Description                                    |
| :------ | :---------------- | :--------------------------------------------- |
| `PRESS` | `PRESS GUI,r`     | Presses one or more keys simultaneously.       |
| `TYPE`  | `TYPE Hello World`| Types the given text.                          |
| `DELAY` | `DELAY 1000`      | Pauses for the given number of milliseconds (1000ms = 1s). |
| `ENTER` | `ENTER`           | Presses the Enter key.                         |

**Supported Keywords:** `GUI` (or `WINDOWS`), `CTRL`, `ALT`, `SHIFT`, `ENTER`, `ESC`, `BACKSPACE`, `TAB`, `CAPS_LOCK`, `DELETE`, `INSERT`, `HOME`, `END`, `PAGE_UP`, `PAGE_DOWN`, `UP`, `DOWN`, `LEFT`, `RIGHT`, `SPACE`, and `F1` through `F12`.

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/techchipnet/ESP32-BLE-HID-GUI/issues).

---

## ⚠️ Disclaimer

This project is intended for educational purposes only. I'm not responsible for any actions or consequences resulting from the use of this code. Users are responsible for ensuring compliance with all applicable laws and regulations when using this project.

---

## 📜 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
