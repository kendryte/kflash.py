# kflash, A Python-based Kendryte K210 UART ISP Utility

## Sample Usage

```bash
# Linux or macOS
python3 kflash.py firmware.bin
python3 kflash.py -t firmware.bin # Open a Serial Terminal After Finish

# Windows CMD or PowerShell
python kflash.py firmware.bin
python kflash.py -t firmware.bin # Open a Serial Terminal After Finish

# Windows Subsystem for Linux
sudo python3 kflash.py -p /dev/ttyS13 firmware.bin # ttyS13 Stands for the COM13 in Device Manager
sudo python3 kflash.py -p /dev/ttyS13 -t firmware.bin # Open a Serial Terminal After Finish
```

## Requirements

- Python3
- PySerial

### Windows

- Download and Install [Python3 at python.org](https://www.python.org/downloads/release/python-367/)
- Download the [get-pip.py at https://bootstrap.pypa.io/get-pip.py](https://bootstrap.pypa.io/get-pip.py)
- Start CMD or PowerShell Terminal and run the following command

 ```bash
 python get-pip.py
 python -mpip install pyserial
 ```

 --------

### macOS

```bash
# Install Homebrew, an awesome package manager for macOS
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew install python
python3 -mpip3 install pyserial
```

 --------

### Ubuntu, Debian

```bash
sudo apt update
sudo apt install python3 python3-pip
sudo pip3 install pyserial
```
 --------

### Fedora

```bash
sudo dnf install python3
sudo python3 -m pip install pyserial
```

 --------

### CentOS

```bash
sudo yum -y install epel-release
sudo yum -y install python36u python36u-pip
sudo ln -s /bin/python3.6 /usr/bin/python3
sudo ln -s /bin/pip3.6 /usr/bin/pip3
sudo pip3 install pyserial
```

## Trouble Shooting

 --------

## Could not open port /dev/tty*: [Errno 13] Permission denied: '/dev/tty*'

> For Windows Subsystem for Linux, you may have to use sudo due to its docker like feature

- Add your self to a dialout group to use usb-to-uart devices by

```bash
sudo usermod -a -G dialout $(whoami)
```

- Logout, and log in.

 --------

## UART Auto Detecting is Not Working, or Select the Wrong UART Port

### Windows

- Check the COM Number for your device at the Device Manager, such as **USB-SERIAL CH340(COM13)**.

```bash
python kflash.py -p COM13 firmware.bin
```

### Windows Subsystem For Linux(WSL)

- Check the COM Number for your device at the Device Manager, such as **USB-SERIAL CH340(COM13)**.

```bash
sudo python3 kflash.py -p /dev/ttyS13 firmware.bin # You have to use *sudo* here
```

### Linux

- Check the USB Device Name, Usually presented as ttyUSB*

```bash
ls /dev/ttyUSB*
```

- It will print :

```bash
$ ls /dev/ttyUSB*
/dev/ttyUSB0
/dev/ttyUSB2
/dev/ttyUSB13
```

- Choose the one you think belongs to your device, or you may try multimule names.

```bash
python3 kflash.py -p /dev/ttyUSB13 firmware.bin
```

### macOS

- Check the USB Device Name, Usually presented as cu.*

```bash
ls /dev/cu.*
```

- It will print :

```bash
$ ls /dev/ttyUSB*
/dev/cu.wchusbserial1410
/dev/cu.wchusbserial1437
/dev/cu.SLAB_USBtoUART2333
```

- Choose the one you think belongs to your device, or you may try multimule names.

```bash
python3 kflash.py -p /dev/cu.wchusbserial1410 firmware.bin
```

#### You may unable to find the device even in the /dev, check the link below for drivers

- For K210 and Sipeed Dan -> [WCH CH34x USB2UART Chip](https://github.com/adrianmihalko/ch340g-ch34g-ch34x-mac-os-x-driver)

 --------
