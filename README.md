# nmi-image-rip
A C64 image saver from NMI wedge.

This is in Turbo Macro Pro format.

I typically assemble the output to the filename "imgrip.o". This assembles to $C000. Thus, it has to be loaded without relocation, and then initialized with SYS49152. OR, much easier, if you have JiffyDOS, you can load and run it with 
 
 £imgrip.o
 
Once initialized, it is wedged into the NMI. You can typically load and run a program that embeds a graphic file. The only supported formats are the VIC-II's native formats, Hires Bitmap and Multicolor Bitmap. 

There are tons of these kinds of images on CSDB (you can search for them) that are packaged as programs. Typically you load and run the program, and it uncompresses the image data and puts it somewhere in memory appropriate for the VIC-II to render. 

After the image is displaying on the screen, press the RESTORE key. This generates an NMI, which triggers the image ripper. The ripper analyzes the CIA for which VIC-II bank is in use, and analyzes the VIC-II's registers for the bitmap mode and the bank it's rendering from. If a Bitmap is not currently being displayed, the Image Ripper stays in memory but it doesn't do anything.

If the image ripper finds a hires bitmap, it will save it to an ArtStudio file called "image.art" on the current device.

If the image ripper finds a multicolor bitmap, it will save it to a Koala file called "image.koa" on the current device.

Typically to leave the program that is showing the image, you can hold STOP and press RESTORE. This warm reboots the C64, which restores the original NMI vectors. To rip another image, you must reload/rerun imgrip.o. If imgrip.o is still in memory you should also be able to reinitialize it by issuing an SYS49152.
