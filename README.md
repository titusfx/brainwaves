# Measuring Brainwaves

Emotiv Plus with Linux and HID library

This project is Forked from https://github.com/nikhiljay/brainwaves

I found some problems and fix it, also use HID ( hidapi cython library ) for hidapy python library (pyhidapi ) use this repo https://github.com/titusfx/CyKITv2

This project uses <a href="https://github.com/openyou/emokit" target="_blank">emokit</a> which is an open source driver used to access the Emotiv Device raw data.

## Extracting the Raw Data

1) Download the repository

```
$ git clone https://github.com/titusfx/brainwaves.git
```
2) Plug in your <a href="https://emotiv.com" target="_blank">Emotiv</a>'s USB dongle.

3) Find the Serial Number of the Emotiv by downloading HIDAPI.

```
$ git clone https://github.com/signal11/hidapi.git
$ cd hidapi
```

4) In the HIDAPI go to the directory that corresponds to your operating system (in my case linux) and run: 

```
$ make -f Makefile-manual
```

5) A hidtest file should be created in the same directory. Open the hidtest to run it. On linux, you must run this using sudo.
```
$ sudo ./hidtest-hidraw 
```

6) The output should be a list of devices that are connected to the computer. Look at the Emotiv device information and copy the Serial Number.

7) In the brianwaves project, go to the emokit directory.

```
$ cd emokit/python/emokit
```

8) Open "emotiv.py" and paste the serial number on line where it says:

```
def __init__(self, display_output=True, serial_number="
```

10) Run the "emotiv.py" file.

```
$ python emotiv.py
```

11) If there are any dependencies ( in my case where pycrypto, bottle, gevent)
 that need to be installed used the "pip" command.

```
$ sudo pip install [missing dependency goes here]
```

12) Install all dependencies until the following error is produced:

```
Traceback (most recent call last):
  File "emotiv.py", line 674, in <module>
    a.setup()
  File "emotiv.py", line 432, in setup
    self.setup_darwin()
  File "emotiv.py", line 537, in setup_darwin
    hidraw = hid.device(0x21a1, 0x0001)
  File "hid.pyx", line 45, in hid.device.__cinit__ (hid.c:1280)
```

9) Turn on the <a href="https://emotiv.com" target="_blank">Emotiv</a> and try again. A succesful output should be printed:

![](http://i.imgur.com/kKuvuHlm.png)

These electrodes in the picture above represent certain parts of the brain shown here:

![](http://i.imgur.com/xTtsqc7m.jpg)
