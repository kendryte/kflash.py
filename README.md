# kflash.py

## USAGE

### Linux

#### Install base tools

Install python3, pip and pyserial.

Under ubuntu, debian:

```bash
sudo apt-get update
sudo apt-get install python3 python3-pip
sudo pip3 install pyserial
```

Under Fedora

```bash
sudo dnf install python3
sudo python3 -m pip install pyserial
```

Under CentOS:

```bash
sudo yum -y install epel-release
sudo yum -y install python36u python36u-pip
sudo ln -s /bin/python3.6 /usr/bin/python3
sudo ln -s /bin/pip3.6 /usr/bin/pip3
sudo pip3 install pyserial
```

#### Add your self to dialout group to use usb-to-uart devices

```bash
sudo usermod -a -G dialout $(whoami)
```

Logout, and login.

#### Check usb device

```bash
ls /dev/ttyUSB*
```

For example, the terminal may output like this:

```bash
/dev/ttyUSB0
```

#### Program k210 board under terminal

```bash
python3 kflash.py --device /dev/ttyUSB0 --baudrate 115200 firmware.bin
```

### Windows

The easiest way is using [kendryte-flash-windows](https://github.com/kendryte/kendryte-flash-windows) or [WSL](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux)

#### Install python3 and pip of python3

- [Download Python : https://www.python.org/downloads/](https://www.python.org/downloads/)
- [Download Pip : https://pypi.python.org/pypi/pip#downloads](https://pypi.python.org/pypi/pip#downloads)

Install python3, and extract pip3 to install it.

#### Program k210 board under console

```bash
python3 kflash.py --device COM3 --baudrate 115200 firmware.bin
```
