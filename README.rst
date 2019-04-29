kflash, A Python-based Kendryte K210 UART ISP Utility
=====================================================

Usage
-----

.. code:: bash

    usage: kflash.py [-h] [-p PORT] [-c CHIP] [-b BAUDRATE] [-l BOOTLOADER]
                     [-k KEY] [-v] [-t] [-n] [-s] -B BOARD
                     firmware

    positional arguments:
      firmware              firmware bin path

    optional arguments:
      -h, --help            show this help message and exit
      -p PORT, --port PORT  COM Port
      -c CHIP, --chip CHIP  SPI Flash type, 0 for in-chip, 1 for on-board
      -b BAUDRATE, --baudrate BAUDRATE
                            UART baudrate for uploading firmware
      -l BOOTLOADER, --bootloader BOOTLOADER
                            bootloader bin path
      -k KEY, --key KEY     AES key in hex, if you need encrypt your firmware.
      -v, --verbose         increase output verbosity
      -t, --terminal        Start a terminal after finish (Python miniterm)
      -n, --noansi          Do not use ANSI colors, recommended in Windows CMD
      -s, --sram            Download firmware to SRAM and boot
      -B BOARD, --Board BOARD
                            Select dev board, kd233 or dan or bit or goD or goE

Attention
---------

Maixgo with openec firmware, BOARD must choose ``-B goE``, and should choose
sencond com port.

With cmsis-dap firmware(before 2019.02.21), BOARD must use ``-B goD``.

You can update `new cmsis-dap firmware <http://blog.sipeed.com/p/352.html>`__, it is same as openec.

For K210 Trainer V0.01b, BOARD must choose ``-B trainer``.

For KD233, BOARD must choose ``-B kd233``, and the jumper for kd233 automatic
download circuit must be set.

Installation
------------

.. code:: bash

    sudo pip3 install kflash

If you receive an error, please try

.. code:: bash

    sudo python -m pip install kflash
    sudo python3 -m pip install kflash
    sudo pip install kflash
    sudo pip2 install kflash

For linux users, first of all, you must add yourself to dialout group.
Or you have to use root permission every time.

.. code:: bash

    sudo usermod -a -G dialout $(whoami)

Sample Usage
------------

.. code:: bash

    # Linux or macOS
    # Using pip
    kflash -B dan firmware.bin
    kflash -B dan -t firmware.bin # Open a Serial Terminal After Finish
    # Using source code
    python3 kflash.py -B dan firmware.bin
    python3 kflash.py -B dan -t firmware.bin # Open a Serial Terminal After Finish

    # Windows CMD or PowerShell
    # Using pip
    kflash -B dan firmware.bin
    kflash -B dan -t firmware.bin # Open a Serial Terminal After Finish
    kflash -B dan -n -t firmware.bin # Open a Serial Terminal After Finish, do not use ANSI colors
    # Using source code
    python kflash.py -B dan firmware.bin
    python kflash.py -B dan -t firmware.bin # Open a Serial Terminal After Finish
    python kflash.py -B dan -n -t firmware.bin # Open a Serial Terminal After Finish, do not use ANSI colors

    # Windows Subsystem for Linux
    # Using pip
    sudo kflash -B dan -p /dev/ttyS13 firmware.bin # ttyS13 Stands for the COM13 in Device Manager
    sudo kflash -B dan -p /dev/ttyS13 -t firmware.bin # Open a Serial Terminal After Finish
    # Using source code
    sudo python3 kflash.py -B dan -p /dev/ttyS13 firmware.bin # ttyS13 Stands for the COM13 in Device Manager
    sudo python3 kflash.py -B dan -p /dev/ttyS13 -t firmware.bin # Open a Serial Terminal After Finish

For fast programming,

.. code:: bash

    # Using pip
    # This will enable opoenec super-baudrate!
    kflash -b 4500000 -B goE firmware.bin
    # Trainer could use 8000000 baudrate!
    kflash -b 8000000 -B trainer firmware.bin
    # Dan could use 3000000 baudrate!
    kflash -b 3000000 -B dan firmware.bin

    # Using source code
    # This will enable opoenec super-baudrate!
    python3 kflash.py -b 4500000 -B goE firmware.bin
    # Trainer could use 8000000 baudrate!
    python3 kflash.py -b 8000000 -B trainer firmware.bin
    # Dan could use 3000000 baudrate!
    python3 kflash.py -b 3000000 -B dan firmware.bin

Execute user code directly in SRAM and view in serial terminal,

.. code:: bash

    # Using pip
    # For `.elf` file
    kflash -b 115200 -B goE -s -t hello_world
    # For `.bin` file
    kflash -b 115200 -B goE -s -t hello_world.bin

    # Using source code
    # For `.elf` file
    python3 kflash.py -b 115200 -B goE -s -t hello_world
    # For `.bin` file
    python3 kflash.py -b 115200 -B goE -s -t hello_world.bin

Requirements
------------

-  python>=3 or python=2.7
-  pyserial>=3.4
-  pyelftools>=0.25

    Python3 is recommended.

Windows Requirements
~~~~~~~~~~~~~~~~~~~~

-  Download and Install `Python3 at python.org <https://www.python.org/downloads/release/python-367/>`__
-  Download the `get-pip.py at https://bootstrap.pypa.io/get-pip.py <https://bootstrap.pypa.io/get-pip.py>`__
-  Start CMD or PowerShell Terminal and run the following command

``bash  python get-pip.py  python -mpip install pyserial``

--------------

macOS Requirements
~~~~~~~~~~~~~~~~~~

.. code:: bash

    # Install Homebrew, an awesome package manager for macOS
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    brew install python
    python3 -mpip3 install pyserial

--------------

Ubuntu, Debian Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: bash

    sudo apt update
    sudo apt install python3 python3-pip
    sudo pip3 install pyserial

--------------

Fedora
~~~~~~

.. code:: bash

    sudo dnf install python3
    sudo python3 -m pip install pyserial

--------------

CentOS
~~~~~~

.. code:: bash

    sudo yum -y install epel-release
    sudo yum -y install python36u python36u-pip
    sudo ln -s /bin/python3.6 /usr/bin/python3
    sudo ln -s /bin/pip3.6 /usr/bin/pip3
    sudo pip3 install pyserial

Trouble Shooting
----------------

Could not open port /dev/tty*: [Errno 13] Permission denied: '/dev/tty*'
------------------------------------------------------------------------

    For Windows Subsystem for Linux, you may have to use sudo due to its docker
    like feature

-  Add your self to a dialout group to use usb-to-uart devices by

.. code:: bash

    sudo usermod -a -G dialout $(whoami)

-  Logout, and log in.

--------------

UART Auto Detecting is Not Working, or Select the Wrong UART Port
-----------------------------------------------------------------

Windows
~~~~~~~

-  Check the COM Number for your device at the Device Manager, such as
   **USB-SERIAL CH340(COM13)**.

.. code:: bash

    python kflash.py -p COM13 firmware.bin

Windows Subsystem For Linux(WSL)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Check the COM Number for your device at the Device Manager, such as
   **USB-SERIAL CH340(COM13)**.

.. code:: bash

    sudo python3 kflash.py -p /dev/ttyS13 firmware.bin # You have to use *sudo* here

Linux
~~~~~

-  Check the USB Device Name, Usually presented as ttyUSB\*

.. code:: bash

    ls /dev/ttyUSB*

-  It will print :

.. code:: bash

    $ ls /dev/ttyUSB*
    /dev/ttyUSB0
    /dev/ttyUSB2
    /dev/ttyUSB13

-  Choose the one you think belongs to your device, or you may try multimule
   names.

.. code:: bash

    # Using pip
    python3 kflash.py -p /dev/ttyUSB13 firmware.bin
    # Using source code
    kflash -p /dev/ttyUSB13 firmware.bin

macOS
~~~~~

-  Check the USB Device Name, Usually presented as cu.\*

.. code:: bash

    ls /dev/cu.*

-  It will print :

.. code:: bash

    $ ls /dev/ttyUSB*
    /dev/cu.wchusbserial1410
    /dev/cu.wchusbserial1437
    /dev/cu.SLAB_USBtoUART2333

-  Choose the one you think belongs to your device, or you may try multimule
   names.

.. code:: bash

    # Using pip
    kflash -p /dev/cu.wchusbserial1410 firmware.bin
    # Using source code
    python3 kflash.py -p /dev/cu.wchusbserial1410 firmware.bin

You may unable to find the device even in the /dev, check the link below for
drivers

-  For K210 and Sipeed Dan -> `WCH CH34x USB2UART Chip <https://github.com/adrianmihalko/ch340g-ch34g-ch34x-mac-os-x-driver>`__
