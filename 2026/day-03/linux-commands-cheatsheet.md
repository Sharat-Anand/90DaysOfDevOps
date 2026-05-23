# Process Management
systemd is the 1st process<br>
systemctl status nginx/docker --to check status of process<br>
systemctl start nginx/docker --- To start any process<br>
systemctl stop nginx/docker ---  To Stop any process<br>
journalctl -u nginx/docker ---- to show all logs of an individual process<br>

# User Management
whoami  ---- shoes which user is active<br>
sudo adduser -m xxx --- Adds user and made directory using -m (Simialr to windows switching)<br>
sudo passwd xxx --- set up password for login<br>
su xxx --- command to enter inside user giving password (opens black bash)<br>
which bash --- which bash currently am i using (usually coloured) gives path<br>
sudo useradd -m yyy -s usr/bin/bash --- to make bash similar to **older coloured style**<br>
cd / > cd home --- ls -l gives list of all users<br>
cat /etc/group --- shows all the user group<br>
sudo addgroup ggg ---making group for user<br>
sudo gpasswd -a xxx ggg   ---adding user inside group. here xxx is added in group ggg along **with permission** gets added<br>
sudo gpasswd -d xxx ggg   ---To remove the user from that group and revoke their permissions. Restart with newgrp current user<br>
sudo usermod -aG docker ubuntu ---Adding an Ubuntu User to the docker Group to **avoid sudo** and have permissions<br>
sudo chown ggg filename.txt ---change the owner of the file from ubuntu to other user<br>
sudo chgrp xxx filename.txt --change group name<br>
# File System
Read (cat)<br>
Write (vim/nano)<br>
Execute (shell/ ./)<br>
mkdir -p devops  -----makes directory **with path** without error even if it exists do not throw error<br>
vim hello.txt > Insert i > write content > Esc > :wq(save and quit)/:q!(exit without saving)<br>
newgrp ubuntu --- changes current active primary group to the group named ubuntu for your current terminal session<br>
-rwxrwxrwx --read write execute for **owner group others** in sets of 3<br>
chmod 777 ---giving all permission / chmod 400 ----giving only read permission<br>

# Volume Mounting
lsblk ---volume/disk all attached to the server shows block with various partition<br>
xvda ---extended version is written in form **/dev/xvda**<br>
df -h ---free disk space in disk and shows mount point<br>
Attach and Mount are 2 different thing. /dev/xvda shows attachment to system<br>
Instance attached to volume is called attaching. Binding volume to a location is called mounting.<br>
EBS(Elastic block store to  to create ssd) ---go to EBS in aws and create multiple volumes.<br>
select volume > Actions > Attach volume to the corrosponding instances(select correct device name) > Check through lsblk<br>
To make volume of EBS into useable volume convert into Physical Volume<br>
Logical volume size can be incraesed or decreased according to the usage<br>

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
Sudo lvm ---become a root user initially. Its a tool to manage LVM having commands for mounting<br>
pvcreate /dev/xvdf /dev/xvdg /dev/xvdh ----create physical volume for 3 ebs volume available in aws<br>
pvs ---- shows the physical volume details<br>

vgcreate  tws_vg  /dev/xvdf  /dev/xvdg ---To create Volume group using 2 physical volume earlier made. initail is the vg nam and then from the source path to be combined<br>
vgs ----shows list of all the volume from group craeted where PV is phy. vol. and LV is Logical vol.<br>

lvcreate -L 10G -n tws_lv tws_vg --- to create logical volume from the volumegroup<br>
lvs --- shows list of all the volume of group created<br>

pvdisplay ---- to display physical volume details<br>
vgdisplay ----- to display volume group details<br>
lvdisplay ---- to displaylogical volume details<br>

# How to mount volumes 
Go to root always<br>
mkdir /mnt/tws_lv_mount --- create a temproary directory which creates a location where volume is mounted<br>
mkfs.ext4 /dev/tws_vg/tws_lv  ---to format the path and create space and make file system<br>
mount /dev/tws_vg/tws_lv /mnt/tws_lv_mount --mount the logical volume to specified location craeted before to bind the path<br>
umount /mnt/tws_lv_mount ---to unmount the volume directory<br>
Now you can use the path to craete directory and work here  /mnt/tws_lv_mount<br>

# Directly mount physical volume to disk mount
No need to go to room <br>
mkdir /mnt/tws_disk_mount ----this is to create space for disk mount directly from phy. vol.<br>
mkfs -t ext4  /dev/xvdh ----file system to mount disk store<br>
mount /dev/xvdh  /mnt/tws_disk_mount --- mounting disk to the destination<br>
df -h --to check all the disk mounted<br>

# Dynamic storage management with EBS(AWS)
Adding extra storage to Logical Volume<br>
lvm > lvextend -L +5G -n /dev/tws_vg/tws_lv <br>
