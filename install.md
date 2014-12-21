## Installing Debian 7 on a Dell XPS

Notes from me, [Eric Mill](https://twitter.com/konklone), as I installed Debian for the first time, onto a new laptop, with sage advice and spiritual guidance from [Paul Tagliamonte](https://twitter.com/paultag).

You will need:

* **A USB drive** with at least 1 GB of space.
* **A USB network connection.** Like a smartphone that can tether a WiFi connection over USB, or a USB WiFi stick.

### You Will Also Need A Computer

I am using a Dell XPS 13, Developer edition, 4th generation, purchased through the Dell Ubuntu program:

> http://dell.com/ubuntu

The Dell Ubuntu program is managed by a friendly, competent team of Linux-friendly folk inside Dell who ensure that your computer will Just Work with Linux. The Dell XPS is used by multiple Debian team members, so your pain points will be theirs, and they will fix things.

Supporting Dell's program is a wonderful thing to do, and it's also just a **great goddamned laptop**.

### You Will Also Need Debian

Debian has `unstable`, `testing`, and `stable` versions.

* `unstable` is the most fresh: the edge.
* `testing` runs 10 days behind `unstable`, and is probably what you want.
* `stable` is (deliberately) quite out of date as it waits for software to prove itself, and because of that is extremely stable. It runs underwater robots.

http://cdimage.debian.org/cdimage/jessie_di_beta_2/amd64/iso-cd/



### Preparing Debian for Installation

First, we'll be flashing the USB drive. From Ubuntu:

* Find the device ID: it will probably look like `/dev/sdb`.
* If the ISO has been renamed to `debian.iso`, and the device is `/dev/sdb`, run:

```bash
sudo dd if=debian.iso of=/dev/sdX
```

* Reboot the computer.
* On boot, **go into the BIOS** by pressing F2 while the Dell logo appears.
* Go to the `Boot` menu.
* Switch the `Boot List Option` to `UEFI`, and the `Load Legacy Option Rom` option to `Disabled`.

![Switch to UEFI](images/install/01-uefi-boot.jpg)

* **Warning:** After you turn on UEFI mode, you will not be able to boot back into whatever you were coming from (e.g. if you change your mind), unless you return here and switch this option back to Legacy Boot.
* Reboot the machine by saving and exiting the BIOS.
* On boot, **go into Boot Options** by pressing F2 while the Dell logo appears.
* Select the USB drive under the UEFI section.

![Choose USB to proceed](images/install/02-boot-to-installer.jpg)

You should soon see the Debian install screen pop up.

### Installing Debian

You should be at the graphical installer screen.

![Graphical installer](images/install/03-installer.jpg)

**General warning:** The installer has "Go Back" options laid throughout the process. It may not always do what you think. While it will usually be fine, and as much as I hate to say it: try to get each step right the first time. If you end up "Going Back" and it doesn't look like you've actually gone back, consider starting over fresh.

**General encouragement:** There's a lot of steps, but this is all super easy. You will be just fine.

* Pick the top option, `Install`.

* Choose your language (e.g. `English`), your country (e.g. `United States`), and your key map (e.g. 'American English').

![Pick your language](images/install/04-language.jpg)

![Pick your location](images/install/05-location.jpg)

![Pick your keymap](images/install/06-keyboard-map.jpg)

* Then it will try to find a network connection. Maybe it'll work with your WiFi, but it failed for me:

![No network connection](images/install/07-no-network.jpg)

* Plug in your USB network connection. Hit `Tab` to highlight `Go Back`, then hit `Enter` to return to this screen, and select `Detect Network Hardware`:

![Menu to retry connection](images/install/08-retry-network.jpg)

* Then enter your hostname, which is essentially your computer name (mine was `erictop`).

![Enter hostname](images/install/09-hostname.jpg)

* When it asks for a domain name, leave it blank and hit Enter.

![Enter blank domain](images/install/10-domain.jpg)

* Enter a password for the `root` user, and verify the password.

![Root password](images/install/11-root-pass.jpg)

![Verify root password](images/install/12-root-verify.jpg)

* Now you'll make a user account. Enter your full name (e.g. `Eric Mill`).

![Enter full name](images/install/13-full-name.jpg)

* And pick a username (e.g. `eric`). This is the user you'll be running as.

![Enter username](images/install/14-username.jpg)

* Enter a password for that user, and verify that password.

![User password](images/install/15-user-pass.jpg)

![Verify user password](images/install/16-user-pass-verify.jpg)

* Pick your time zone.

![Pick a timezone](images/install/17-clock.jpg)

### Setting up your disk

Now you'll be asked about disk stuff. This can be intimidating, but don't worry about it.

I'm going for **full disk encryption**. The Debian installer makes this super easy. The downsides are:

* You'll enter a password when you boot your computer up, or resume from hibernation. (Not from ordinary sleep.)
* Can add some slight latency on some kinds of disk writes. This isn't a common problem, and you shouldn't notice much of anything in practice.
* Will make the _install_ process take a couple hours, as it first erases every block of the disk.

The upside is your **entire disk is goddamn encrypted**, which makes you more safe from attackers the world over. And **it's so easy**: besides the boot password, there's no impact on usability. I strongly recommend it.

* To encrypt, go with the third option:

![Choose encryption](images/install/18-pick-encryption.jpg)

* Just put everything on one partition.

![All on one partition](images/install/19-all-on-one-partition.jpg)

* It will ask you to confirm which disk you want to encrypt and write Debian to. Make sure you pick your actual hard drive, not the USB flash drive.

![Confirm the disk](images/install/20-confirm-the-disk.jpg)

* It'll ask you to really confirm what you're about to do:

![Really confirm it](images/install/21-really-confirm.jpg)

* Then prepare for the disk erasing to take a long time.

![Taking forever to erase the disk](images/install/22-taking-forever.jpg)

* When it finishes, enter in the disk encryption passphrase, and verify it.

![Enter encryption passphrase](images/install/23-encryption-passphrase.jpg)

![Verify encryption passphrase](images/install/24-encryption-passphrase-verify.jpg)

* Then you'll get 2 confirmation prompts in sequence, to confirm that you want to write the partitions to disk. Go for it.

![Confirm partitioning once](images/install/25-finish-partitioning.jpg)

![Confirm partitioning twice](images/install/26-confirm-partitioning.jpg)

* This will begin installing the base system.

![Install base system](images/install/27-installing-base.jpg)

* First, it'll ask you to pick the country it should look for a close Debian archive in.

![Pick a country](images/install/28-pick-mirror-1.jpg)

![Pick a country 2](images/install/29-pick-mirror-2.jpg)

* Then, it'll offer you some specific mirrors. Pick whatever.

![Pick a mirror](images/install/30-pick-specific-mirror.jpg)

* It'll ask you to pick a proxy. You can leave it blank and hit `Enter`.

![Pick a proxy](images/install/31-proxy.jpg)

* It will ask you whether you'd like to participate in submitting weekly analytics to the Debian team about your packages. As of version 1.6 of `popcon`, which is contained in the `.iso` I downloaded, this information is encrypted, so I elected to participate.

![Participate in analytics](images/install/32-statistics.jpg)

* It will ask about what pieces of the system you'd like to install. The defaults are fine: "Debian desktop", "GNOME", "print server", "standard system utilities".

![The parts of Debian you need](images/install/33-tasksel.jpg)

* When it finishes, you should be done!

![You're done!](images/install/34-done.jpg)

Reboot the computer.

### Debian: First Boot


Log in, test touch screen

* su into root
* apt-get install sudo
* adduser [eric] sudo
* log out, log in

* edit /etc/apt/sources.list
  - add 'contrib non-free' to each entry ending in 'main'
* sudo apt-get update
* sudo apt-get install firmware-iwlwifi
* reboot

* set gnome scaling factor to your preference (1.25)
* set iceweasel scaling factor
* set chrome scaling factor

### Making it home

* I like keyboard shortcuts
* static workspaces

extensions

* extensions.gnome.org WHAT
* alternate tab

### Graphical boot

If you want your boot to look nicer, and to enter in your disk decryption password in a clean, well-lighted place, then you need to [install Plymouth](https://miguelmenendez.pro/en/articles/install-plymouth-debian-graphical-boot-animation-while-boot-shutdown.html).

Install Plymouth:

```bash
sudo apt install plymouth plymouth-themes
```

Then edit `/etc/initramfs-tools/modules` and add the following lines:

```
# KMS
  intel_agp
  drm
  i915 modeset=1
```

Then edit `/etc/default/grub` and add this line:

```
GRUB_GFXMODE=1920x1080
```

And **edit** the `GRUB_CMDLINE_LINUX_DEFAULT` line to read:

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
```

Update Grub to pick up the changes:

```bash
update-grub2
```

Set the default theme to `lines`:

```bash
/usr/sbin/plymouth-set-default-theme lines
```

Apply the changes:

```bash
update-initramfs -u
```

And reboot! You should see a nice graphical interface when it's time to enter your disk password. The lines background should even animate for a second during the decryption.




### TODO

* fill in the rest!

* get ubuntu fonts
* swap ctrl + fn keys
* why won't Delete delete things
* how do I get two-dimensional virtual workspaces
* how do I get Alt+Click to grab window
* test out u2f instructions
  - if they work, update blog post to say debian also
* update ubuntu repo to point to debian repo

* disable soft keyboard
