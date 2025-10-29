# PandaKnomiDIY – Unofficial DIY Project

> ⚠️ **Please support BTT/BIQU by purchasing the [official Panda Knomi](https://biqu.equipment/products/panda-knomi).**  
> This project is for educational purposes only. OTA updates and some features may not work like the official product.

---

## 🌟 About the Project

The [official Panda Knomi](https://biqu.equipment/products/panda-knomi) is a compact device that visually displays your printer's status.  
It uses an **ESP32-WROVER-E** (with 16 MB flash memory) and a **round TFT LCD display**.

I wanted to see if it was possible to run the same firmware on a regular ESP32-WROVER-E module with a compatible TFT round display — and it turns out, it is!

---

## 🧩 Challenges I Encountered

1. **ESP32 Flash Size:**  
   It's not easy to find an ESP32-WROVER-E with 16 MB flash, so I used a 4 MB version.

2. **Partition Layout:**  
   I reverse-engineered the layout by examining the [KNOMI (non-Panda) repository](https://github.com/bigtreetech/KNOMI).

3. **Bootloader:**  
   Since the bootloader is not open source, I compiled one using the KNOMI source code.

4. **GIF File Sizes:**  
   I optimized the GIFs using a GIF compression tool to keep the image file under ~1.7 MB to fit into the SPIFFS.

---

## 🔧 Parts List

1. **ESP32-WROVER-E**  
   [AliExpress Link](https://de.aliexpress.com/item/1005006068563165.html)

2. **1.28" Round TFT LCD Display (240x240, 3.3V RGB)**  
   [AliExpress Link](https://de.aliexpress.com/item/1005006430905595.html)

---

## 📌 Pinout

![ESP32 DevKitC v4 Pin Layout](https://github.com/drbeat/PandaKnomiDIY/blob/main/esp32_devkitC_v4_pinlayout.jpg)

| ESP32-WROVER-E Pin | TFT Display Pin |
|--------------------|-----------------|
| 3.3V               | VCC             |
| GND                | GND             |
| GPIO 18            | SCL             |
| GPIO 23            | SDA             |
| GPIO 19            | DC              |
| GPIO 5             | CS              |
| GPIO 4             | RST             |

---

## 💾 Firmware

You’ll need the official **Panda Knomi firmware**, as it is closed source.  
You can find it in the [PandaKnomi GitHub repository](https://github.com/bigtreetech/PandaKnomi) – version **v1.0.5** is recommended.  
Other versions have not been tested.

---

## 🔥 Flashing the Firmware

### via ESPTool

1. Download and install [esptool](https://github.com/espressif/esptool).
2. Place all firmware files (`bootloader.bin`, `partitions.bin`, `panda_knomi_v1.0.5.bin`, `images.img`) into the same folder.
3. Flash the firmware using the following command:

    ```bash
    esptool.py write_flash \
      0x1000 bootloader.bin \
      0x8000 partitions.bin \
      0x10000 panda_knomi_v1.0.5.bin \
      0x240000 images.img \
      --flash_size 4MB
    ```

### via WEB Flasher

1. Go to https://esptool.spacehuhn.com/
2. use this settings ![weblfash](https://github.com/drbeat/PandaKnomiDIY/blob/main/web%20flash.png)

---
