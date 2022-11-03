# Projects
### Arch Linux
### System Administration
### Madison Fischer

## Methodology
### Part 1: Installing Arch Linux

When I got confused during the project, I used this link to guide me through the project https://linuxconfig.org/install-arch-linux-in-vmware-workstation#:~:text=First%2C%20download%20the%20Arch%20Linux,and%20then%20New%20Virtual%20Machine%20.&text=Under%20Install%20Operating%20System%20from,Linux%20ISO%20then%20click%20next%20.&text=Click%20Linux%20under%20Guest%20Operating%20System%20.

First, once you install the ISO, you have to check the SHA1 hash of the file to ensure you downloaded the correct file. To do that, you run the command  shasum -a and then the file name in the terminal. Then you check the SHA 1 hash in the terminal with the SHA 1 has provided in a file from the download page.

The keyboard is defaulted into US, so that doesn’t need to be changed. But can be changed by typing ls/usr/share/kbd/keymaps/**/*.map.gz

Then you have to verify the boot mode and ensure that it’s in UEFI mode. To do that, you run the command `ls/sys/firmware/efi/efivars`

Then you check if the vm is connected to the internet with the command ip link

Then we verify the connection by the command `ping archlinux.org`

Then we check if the system clock is updated with `timedatectl status`

-	Got confused at this next step and had to google to find what command to type

Then to make the partition, we run `cfdisk /dev/sda` and then we select gpt for the label type

We then press Enter to select New and then type 500M and press Enter to create the EFI partition. We then use the right arrow to select Type and change the type to EFI System

We then press down to select Free space and press Enter on New to create sda2 and use the  (x86-64)

We then format the partitions first by doing `mkfs.ext4 /dev/sda2`

We then format the EFI partition system by doing `mkfs.fat -F 32 /dev/sda1`

We then mount the root partition by doing `mount /dev/sda2 /mnt`

We then mount the EFI partition by doing `mount –mkdir /dev/sda1 /mnt/not`

We then install the essential packages by running `pacstrap -K /mnt base linux linux-firmware`

We then created an fstab file with the command `genfstab -U /mnt >> /mnt/etc/fstab`

We then change the root into a new system by doing `arch-chroot /mnt`

-	Had an issue with knowing what time zone I was in

We then set the time zone by doing `ln -sf /usr/share/zoneinfo/US/Chicago /etc/localtime`

Next we install nano by running `pacman -S nano` 

Now we need to edit the locale gen by running `locale-gen`

Then we create the locale.conf file by running `nano /etc/locale.conf` and we add LANG=en_US.UTF-8

We then edit /etc/hostname by running `nano /etc/hostname` and adding archvm, our network name

Then we edit /etc/hosts with `nano /etc/hosts` and add archvm to it

We then need to configure the networks

First by running `systemctl enable system-networkd`

Then run `systemctl enable system-resolved`

Then we find out network interface by running `ip addr`

We then find out we have the interface of ens32

Next, we edit a certain file by running `nano /etc/system/network/20-wired.network`

We then add [Match] Name=ens32 [Network] DHCP=yes

Next we set the password by typing passwd and creating our password 

We then install intel microcode by typing `pacman -S intel-ucode`

Next we install the boot loader

We do that by first installing grub and efibootmgr by using the command `pacman -S grub efibootmgr`

We install grub bootloader to the EFI partition with the command `grub-install –target=x86_64-efi –efi-directory=/boot –bootloader-id=GRUB`

We then generate the main grub configuration by running `grub-mkconfig -o /boot/grub/grub.cfg`

### Part 2: Installing LXDE
We first install LXDE by running `Pacman -S lxde`

We then have to nano into the xinitrc file with `Nano ~/.xinitrc`

Then we add execstartlxde to the file and then save it

We then have to enable LXDE by running `Systemctl enable lxde`

We then start LXDE by running `Systemctl start lxde` 

### Part 3: Create a User

We first add the user by running `useradd Codi`

We then set the password for Codi by running `passwd Codi` and set the password for Codi

Then we have to add Codi to the group wheel in order to give him sudo privileges by running `usermod -aG wheel codi`

Then you have to nano into a document by doing `nano /etc/sudoers`

Then delete the # from the %wheel ALL=(ALL) ALL statement

Repeat for yourself user

![Users](/listofusers.png)

![User Privileges](/userpriv.png)

### Part 4: Install ZSH

To install zsh, you do `pacman -S zsh`

To access zsh, you simply type `zsh`

### Part 5: Install SSH

To install ssh, you first run `pacman -Sy`

Then you run `pacman -S openssh`

You then have to enable ssh by running `systemctl enable sshd`

You can check the status of that by running `systemctl status sshd`

### Part 6: Add Color

To add color to pacman, you run `sed -I ‘s/#Color/Color/g’ /etc/pacman.conf`

To add color to nano, you first `nano  /etc/nanorc` and the delete the # before the statement “include “/usr/share/nano/*.nanorc”

![Colors](/colors.png)

### Part 7: Aliases

To add aliases, you do “alias name = ‘command’”

For example alias c= ‘clear’

### Part 8: Installing a Browser 

`Pacman -Syu firefox` is the command to use to install Firefox

### Project 2 - Docker Project
### System Administration


I used this source for installing WordPress: https://www.hostinger.com/tutorials/run-docker-wordpress
I used this source to look up IP address: https://www.linuxtrainingacademy.com/determine-public-ip-address-command-line-curl/

We installed docker and docker compose in class via the Powerpoint Slides 

### Installing WordPress 

Once docker and docker compose are installed, you first need to check you are on the right version with the command `docker compose -version`

Then once you've checked the version, you make a directory called 'wordpress' with the command `mkdir wordpress`

Then you have to cd into the wordpress directory with the command `cd wordpress`

After that, I chose to use VS Code to create my .yml file, then I inserted the info that I got from my source into the .yml file. I did change the port number from 8000 to 8080 because of some issues I was having with port 80000

Then to finish the installation of wordpress, I put in the command `docker compose up -d` which finished the install of wordpress 

* I ran into some issues of the port 8080 not connection properly, I asked Codi and I found out that i had to use my ip address instead of localhost in the URL

Then I had to run the link http://10.10.1.111:8080/ to open WordPress. 

Then I entered my credentials and made a username and password

Then I was on the main WordPress website 

![Main Page](/mainWordpresspage.png)

![Successful Login](/successfullogin.png)

