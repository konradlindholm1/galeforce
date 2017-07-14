# Galeforce

Galeforce is a minimal patch to the standard Google Wifi image, enabling ssh access.

## How to build image

If you're on a reasonably modern Linux system, you can simply run:

```
./patch-image.sh gale
```

If however you're on Windows or Mac, you'll need to use Vagrant (unfortunately
Docker for these systems don't have the necessary functions in their xhyve kernels to map loop devices properly):

```
vagrant up
vagrant ssh
cd /vagrant
./patch-image.sh gale
```

Once completed (by either method), you can copy this image to a USB stick:

```
sudo dd if=output/gale.bin of=/dev/<usbdevice> bs=1m
```

## How to apply image

You'll have to put the Google Wifi into developer mode:

![Alt text](http://i.imgur.com/iCPe0WO.jpg "Google WIfi")

1. Unscrew the single screw on the bottom
2. Insert a very slim blade or screwdriver to ease out the base cover
3. Insert a USB-C adapter with [Power Delivery](https://www.amazon.co.uk/s/ref=nb_sb_noss?url=search-alias%3Dcomputers&field-keywords=usb+c+adapter+power+delivery&rh=n%3A340831031%2Ck%3Ausb+c+adapter+power+delivery)
4. Press reset button on the back until light blinks orange (16 seconds)
5. Once blinking orange, hit the tiny bubble switch (SW7 on the board)
6. Device will start blinking purple and restart
7. Wait until device restarts and starts blinking purple again
8. Plug in USB stick
9. Hit bubble switch again
10. Wait about five minutes until device pulsing purple (device shows no lights while flashing)

Once installed you can then:

```
ssh root@192.168.86.1 (password changeme)
```

```
localhost ~ # uname -a
Linux localhost 3.18.0-14565-g46be31c1033f #1 SMP PREEMPT Fri Jun 2 14:42:21 PDT 2017 armv7l ARMv7 Processor rev 5 (v7l) Qualcomm (Flattened Device Tree) GNU/Linux

localhost ~ # cat /etc/lsb-release
CHROMEOS_AUSERVER=https://tools.google.com/service/update2
CHROMEOS_BOARD_APPID={9BC3D9F3-D113-8EA2-42D6-F2CDB8189814}
CHROMEOS_CANARY_APPID={90F229CE-83E2-4FAF-8479-E368A34938B1}
CHROMEOS_DEVSERVER=
CHROMEOS_RELEASE_APPID={9BC3D9F3-D113-8EA2-42D6-F2CDB8189814}
CHROMEOS_RELEASE_BOARD=gale-signed-mpkeys
CHROMEOS_RELEASE_BRANCH_NUMBER=40
CHROMEOS_RELEASE_BUILDER_PATH=gale-release/R59-9460.40.5
CHROMEOS_RELEASE_BUILD_NUMBER=9460
CHROMEOS_RELEASE_BUILD_TYPE=Official Build
CHROMEOS_RELEASE_CHROME_MILESTONE=59
CHROMEOS_RELEASE_DESCRIPTION=9460.40.5 (Official Build) stable-channel gale
CHROMEOS_RELEASE_NAME=Chrome OS
CHROMEOS_RELEASE_PATCH_NUMBER=5
CHROMEOS_RELEASE_TRACK=stable-channel
CHROMEOS_RELEASE_VERSION=9460.40.5
DEVICETYPE=OTHER
GOOGLE_RELEASE=9460.40.5
HWID_OVERRIDE=GALE DOGFOOD
```

## Busybox

I've also put busybox on there:

```
localhost ~ # ln -s /bin/busybox /bin/vi
localhost ~ # vi
```

# Change the password (really)

```
localhost ~ # passwd
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```