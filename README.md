# Deviation_F7
Install Deviation (nightly build) on an F7

I have an old Devo F7 and have some receivers, so I wanted to have a better firmware and tried Deviation, which was complex to install.
These are my notes on installing it.
There was this forum entry that unlocked everything https://www.deviationtx.com/forum/6-general-discussions/5454-devo-f7-deviationtx-firmware
```
Replied by Jhavent222 on topic Devo F7 - DeviationTX firmware
Yes, I have. I used the Deviation Uploader and not dfuse. I also got 4.0.1. What I did was used deviation Uploader 9.0 and plugged in Devo f7 and held ext while powering on. This brings you to software update screen. Then I uploaded the version 4.0.1 to deviation Uploader and installed it in my remote. THIS IS NOT THE LAST STEP! Now you hold ent while powering on to bring you into USB mode. When you look at the Devo F7 drive there should be a file called Devo fs. What you need to do is delete that file from the drive. After doing this go back to the zip folder for 4.0.1 and copy the file devo Fs. Lastly go back to The Devo F7 drive and paste it in. Now you can unplug the remote and start using deviation. Good Luck
```

This indicated that the issue was the devo.fs was bad from the Uploader install.

I was installing the nightly build of 5.0 as the 4.1 builds are nolonger accessable.
deviation-devof7-v5.0.0-c84450e.zip

This was not working for me so as a last try I installed what seemed like a very limited new bootloader on the F7, this made a big difference as when I added the deviation build with Uploader it now started mounting as a real file system on Win11. Thus I could replace the devo.fs from the mounted transmitter with the one from the zip.

To install the bootloader I usedthe 12kb devof7bootloader.bin from https://drive.google.com/drive/folders/0B3y72n5Y9u-kfmxMdlY0RmVQdkNMMGRMODgwWGZqQUdBLUMxWTVfbGFRZXJ1LWFKTDM1enc?resourcekey=0-fHWoA5L9WpSonwB8vV5u7A

Using the dfu-util-static.exe from dfu-util.sourceforge.net
Then ran 
```
C:\Users\cdegroot\Desktop\Walkera>dfu-util-static.exe -a 0 -s 0x08000000:leave -D devof7bootloader.bin
dfu-util 0.8

Copyright 2005-2009 Weston Schmidt, Harald Welte and OpenMoko Inc.
Copyright 2010-2014 Tormod Volden and Stefan Schmidt
This program is Free Software and has ABSOLUTELY NO WARRANTY
Please report bugs to dfu-util@lists.gnumonks.org

Invalid DFU suffix signature
A valid DFU suffix will be required in a future dfu-util release!!!
Opening DFU capable USB device...
ID 0483:df11
Run-time device DFU version 011a
Claiming USB DFU Interface...
Setting Alternate Setting #0 ...
Determining device status: state = dfuDNLOAD-IDLE, status = 0
aborting previous incomplete transfer
Determining device status: state = dfuIDLE, status = 0
dfuIDLE, continuing
DFU mode device DFU version 011a
Device returned transfer size 1024
DfuSe interface name: "Internal Flash  "
Downloading to address = 0x08000000, size = 12288
Last page at 0x08002fff is not writeable
```
Note it returned an error, but wrote enough of the bootloader for me to rerun the Uploader, find the OS mount and replace the devo.fs.
