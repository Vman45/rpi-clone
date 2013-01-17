
rpi-clone is a shell script that will back up (clone using dd and rsync)
a running Raspberry Pi file system to a destination SD card 'sdN' plugged
into a Pi USB port (via a USB card reader).
I use it to maintain backups of several Pi SD cards I have and
the backup SD cards can be a different size from the booted SD card.

rpi-clone can clone the running system to a new SD card or can incrementally
rsync to existing backup Raspberry Pi SD cards.  During the clone to new SD
cards, rpi-clone gives you the opportunity to give a label name to the
partition 2 so you can keep track of which SD cards have been backed up.
Just stick a corresponding label on each SD card you have and you can look
up the last clone date for that card in the rpi-clone log file
/var/log/rpi-clone.

If the destination SD card has an existing partition 1 and partition 2
matching the running partition types, rpi-clone assumes (unless using the
-f option) that the SD card is an existing backup with the partitions
properly sized and set up for a Raspberry Pi.  All that is needed
is to mount the partitions and rsync them to the running system.

If these partitions are not found (or -f), then rpi-clone will ask
if it is OK to initialize the destination SD card partitions.
This is done by a partial 'dd' from the running booted device /dev/mmcblk0
to the destination SD card /dev/sdN followed by a fdisk resize and mkfs.ext4
of /dev/sdN partition 2.  This creates a completed partition 1 containing
all boot files and an empty but properly sized partition 2 rootfs.
The SD card  partitions are then mounted on /mnt/clone and rsynced to the
running system.

You should avoid running other disk writing programs when running rpi-clone,
but I find rpi-clone works fine when I run it from a terminal window.
Although I usually do quit my browser first because a browser can be
writing many temporary files.

rpi-clone must be run as root.

rpi-clone is on github, get it with:

git clone https://github.com/billw2/rpi-clone.git 



Bill Wilson
billw@gkrellm.net
