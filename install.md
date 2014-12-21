## Debian 7 on a Dell XPS

I'm using a Dell XPS 13, purchased through the Dell Ubuntu program:

> http://dell.com/ubuntu

It's difficult to figure out how to get started with Debian from the official sources. Avi Kelman kindly maintains a pointer to the version of Debian you probably want:

> https://fiendish.github.io/The-Debian-Gotham-Needs/

It's the 64-bit version, with **non-free software enabled** (so that your wireless card will work). You can certainly go with other install paths for Debian. I elected to use the one I thought would give me

Downloading an ISO

Flash to USB

dd if=debian.iso of=/dev/sdX

Restarted, went into BIOS, enabled Boot List Options -> UEFI Mode

  THIS RENDERS SYSTEM NOT BOOTABLE WITHOUT CONTINUING (unless you change your mind)

Restarted, went into Boot Options, selected the USB drive in the UEFI section

English

United States

-> Tried to find wireless
-> Plugged in phone to USB tether
-> Tab -> Go Back
-> Detect network hardware
-> hostname
-> domain (blank)
-> password for root
-> User Name
-> username
-> password for username
-> Time zone

Partitions

LVM encrypted (guided)
All on one partition
Okay let's go

