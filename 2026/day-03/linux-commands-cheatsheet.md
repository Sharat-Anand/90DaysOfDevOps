# Process Management
systemd is the 1st process
systemctl status nginx/docker --to check status of process
systemctl start nginx/docker --- To start any process
systemctl stop nginx/docker ---  To Stop any process
journalctl -u nginx/docker ---- to show all logs of an individual process

# User Management
whoami  ---- shoes which user is active
sudo adduser -m xxx --- Adds user and made directory using -m (Simialr to windows switching)
sudo passwd xxx --- set up password for login
su xxx --- command to enter inside user giving password (opens black bash)
which bash --- which bash currently am i using (usually coloured) gives path
sudo useradd -m yyy -s usr/bin/bash --- to make bash similar to **older coloured style**
cd / > cd home --- ls -l gives list of all users
cat /etc/group --- shows all the user group
sudo addgroup ggg ---making group for user
sudo gpasswd -a xxx ggg   ---adding user inside group. here xxx is added in group ggg along **with permission** gets added
sudo gpasswd -d xxx ggg   ---To remove the user from that group and revoke their permissions. Restart with newgrp current user.
sudo usermod -aG docker ubuntu ---Adding an Ubuntu User to the docker Group to **avoid sudo** and have permissions
sudo chown ggg filename.txt ---change the owner of the file from ubuntu to other user

# File System
Read (cat)
Write (vim/nano)
Execute (shell/ ./)
mkdir -p devops  -----makes directory **with path** without error even if it exists do not throw error
vim hello.txt > Insert i > write content > Esc > :wq(save and quit)/:q!(exit without saving)
newgrp ubuntu --- changes current active primary group to the group named ubuntu for your current terminal session
-rwxrwxrwx --read write execute for **owner group others** in sets of 3
chmod 777 ---giving all permission / chmod 400 ----giving only read permission

# Volume Mounting
lsblk ---volume/disk all attached to the server shows block with various partition
xvda ---extended version is written in form **/dev/xvda**
df -h ---free disk space in disk and shows mount point
Attach and Mount are 2 different thing. /dev/xvda shows attachment to system
Instance attached to volume is called attaching. Binding volume to a location is called mounting.
EBS(Elastic block store to  to create ssd) ---go to EBS in aws and create multiple volumes.
select volume > Actions > Attach volume to the corrosponding instances(select correct device name) > Check through lsblk
To make volume of EBS into useable volume convert into Physical Volume
Logical volume size can be incraesed or decreased according to the usage

            LVM(Logical Volume Manager)
       ------------Logical Volume-----------------------
       --------        ---------             ----------
       | 10GB  |       |  6GB   |            |         |
       ---------       ----------            -----------
           |                |                      |
           |                |                      |
      ------------------------------------------------------
      |               Volume Group                          |
      |                                                     |
      -------------------------------------------------------
           |                 |                      |
           |                 |                      |
        --------        ---------             ----------
        |  10G  |       |  12G   |            | 11 GB   |
        ---------       ----------            -----------
        --------------Physical volume-------------------

# Logical Volume Manager (LVM)
Sudo lvm ---become a root user initially. Its a tool to manage LVM having commands for mounting
pvcreate /dev/xvdf /dev/xvdg /dev/xvdh ----create physical volume for 3 ebs volume available in aws
pvs ---- shows the physical volume details

vgcreate  tws_vg  /dev/xvdf  /dev/xvdg ---To create Volume group using 2 physical volume earlier made. initail is the vg nam and then from the source path to be combined
vgs ----shows list of all the volume from group craeted where PV is phy. vol. and LV is Logical vol.

lvcreate -L 10G -n tws_lv tws_vg --- to create logical volume from the volumegroup
lvs --- shows list of all the volume of group created

pvdisplay ---- to display physical volume details
vgdisplay ----- to display volume group details
lvdisplay ---- to displaylogical volume details

# How to mount volumes 
Go to root always
mkdir /mnt/tws_lv_mount --- create a temproary directory which creates a location where volume is mounted
mkfs.ext4 /dev/tws_vg/tws_lv  ---to format the path and create space and make file system
mount /dev/tws_vg/tws_lv /mnt/tws_lv_mount --mount the logical volume to specified location craeted before to bind the path
umount /mnt/tws_lv_mount ---to unmount the volume directory
Now you can use the path to craete directory and work here  /mnt/tws_lv_mount

# Directly mount physical volume to disk mount
No need to go to room 
mkdir /mnt/tws_disk_mount ----this is to create space for disk mount directly from phy. vol.
mkfs -t ext4  /dev/xvdh ----file system to mount disk store
mount /dev/xvdh  /mnt/tws_disk_mount --- mounting disk to the destination
df -h --to check all the disk mounted

# Dynamic storage management with EBS(AWS)
Adding extra storage to Logical Volume
lvm > lvextend -L +5G -n /dev/tws_vg/tws_lv 
