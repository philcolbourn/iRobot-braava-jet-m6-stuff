# iRobot-braava-jet-m6-stuff
What I know about SoC and USB interface

# History
My Braava died - water ingress into sealed SoC/camera module.

When battery is inserted, it boots for about 30s and then there is one or two beeps and LED ring lights up red.

After this I get a white LED ring followed by one or two beeps and red ring again.

This repeats forever it seems.

Sometimes beeps seem to be different tones.

![signal-2024-01-21-13-49-02-726](https://github.com/philcolbourn/iRobot-braava-jet-m6-stuff/assets/3045809/9a31cabf-b56e-4d19-9dd9-6d71920ec42b)

![signal-2024-01-21-13-52-14-124](https://github.com/philcolbourn/iRobot-braava-jet-m6-stuff/assets/3045809/a948ef03-ed33-4800-8689-a18e1771260b)


# Board
Board is built from a number of chips from Qualcomm including APQ8009.

![signal-2024-01-21-19-43-52-000](https://github.com/philcolbourn/iRobot-braava-jet-m6-stuff/assets/3045809/c9358091-f259-4433-827c-06f80d5e0a15)

![signal-2024-01-21-19-43-41-634](https://github.com/philcolbourn/iRobot-braava-jet-m6-stuff/assets/3045809/32837b88-8b1a-4589-933b-24c2fac77792)

FCC info and pictures: https://fccid.io/UFEAXE-Y1

Board has a number of labelled pads: VBUS, FUB/FU8, GND, DM, DP, PWR, USB_DL, VIN_4.2, V_1.6 and on back: USB_ID and CAM_GPO

V_1.6 has 1.6V on it.

VIN_4.2 has about 4.2V on it.

# USB Micro-B
5 of these pads can be used to add an USB micro-b socket: VBUS, DM, DP, USB_ID, and GND.

![signal-2024-01-24-20-27-45-911](https://github.com/philcolbourn/iRobot-braava-jet-m6-stuff/assets/3045809/5ccda293-376b-4b41-8aa2-4d9d6804301f)


USB_ID is not strictly needed as if left open USB operates in device mode.

But noting a USB_DL (download?) pad, there may be a way to download firmware to SoC by plugging in a USB stick on a OTG adapter that connects USB_ID to GND.

To be investigated if USB provides power. May need to use VIN_4.2 pad to provide power. Perhaps PWR pad has some part in this.

A standard micro usb PC cable can then be used to connect to board.

![signal-2024-01-24-20-27-13-131](https://github.com/philcolbourn/iRobot-braava-jet-m6-stuff/assets/3045809/7c8c1f7f-3e8e-40fa-a3e5-71ba857f979b)


![signal-2024-01-24-20-27-24-285](https://github.com/philcolbourn/iRobot-braava-jet-m6-stuff/assets/3045809/975a0d57-b531-4b78-976a-937314e418ff)


Once connected to linux, I get this from dmesg:

usb 3-2: new full-speed USB device number 23 using xhci_hcd

usb 3-2: not running at top speed; connect to a high speed hub

usb 3-2: New USB device found, idVendor=05c6, idProduct=9091, bcdDevice= 3.18

usb 3-2: New USB device strings: Mfr=1, Product=2, SerialNumber=3

usb 3-2: Product: APQ8009-MTP _SN:1EDBC04E

usb 3-2: Manufacturer: Android

usb 3-2: SerialNumber: 2aa0148a

rndis_host 3-2:1.0 usb0: register 'rndis_host' at usb-0000:00:14.0-2, RNDIS device, 32:89:5c:48:ba:f3

# Android?
Why might Manufacturer be reported as Android?

Perhaps Braava jet m6 runs android?

# Ethernet port
I also get a usb0 ethernet port:

usb0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500

        ether 32:94:22:e8:ca:70  txqueuelen 1000  (Ethernet)

        RX packets 0  bytes 0 (0.0 B)
        
        RX errors 0  dropped 0  overruns 0  frame 0
        
        TX packets 203  bytes 25744 (25.7 KB)
        
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

However, to date, I have not seen a packet on this interface.


