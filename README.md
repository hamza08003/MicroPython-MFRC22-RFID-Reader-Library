# MicroPython-MFRC522-RFID-Reader-Library
This repository contains a library code for the MFRC522 RFID module interface in Mciro-Python. The MFRC522 is a widely used RFID module that allows communication with contactless RFID cards or keychains.It provides functionalities for communication and interaction with MFRC522 RFID cards, including reading and writing data blocks and authentication etc. The library is compatible with various microcontroller platforms.

<br>

## ℹ️ Introduction

This README provides instructions on how to utilize the MFRC522 Python library for interacting with MFRC522 RFID modules. It walks you through the necessary steps to integrate this library into your project and use it for reading and writing RFID cards.

<br>

## ⚙️ Usage

### 1. Initializing the MFRC522 Module

First, import the necessary modules and create an instance of the MFRC522 class by passing all the RFID Reader Pin Numbers Connected to Micro-Controller:

```python
from mfrc522 import MFRC522
# Constructor - General Syntax
reader = MFRC522(sck, mosi, miso, rst, cs, baudrate=1000000, spi_id=0)
# Example
reader = MFRC522(cs=5, sck=6, mosi=7, miso=4, rst=22)
```

Now, we can use this *MFRC22* object to read and perform different operations using RFID Reader


### 2. Here is the Code for Reading RFID Tag ID using `MFRC522` module

```python
from machine import Pin
from mfrc522 import MFRC522
import utime

pin_SDA = 5
pin_SCK = 6
pin_MOSI = 7
pin_MISO = 4
pin_RST = 22

reader = MFRC522(cs=pin_SDA, sck=pin_SCK, mosi=pin_MOSI, miso=pin_MISO, rst=pin_RST)

def read_rfid_tag():
    reader.init()
    reader_req__stat, _ = reader.request(reader.REQIDL)
    if reader_req__stat == reader.OK:
        print("Tag Detected, Scanning....")
        utime.sleep(1)
        (tag_read__stat, uid) = reader.SelectTagSN()
        if tag_read__stat == reader.OK:
            print("Tag Successfully Scanned")
            utime.sleep(1)
            card_id = str(int.from_bytes(bytes(uid), "little"))
            print("Tag ID: " + card_id)
            utime.sleep(2.5)
            print("\nBring TAG Closer for Scanning....")

def main():
    while True:
        read_rfid_tag()

if __name__ == "__main__":
    main()
