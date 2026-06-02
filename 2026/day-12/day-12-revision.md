# Process Management
systemctl status nginx/docker --to check status of process<br>
systemctl start nginx/docker --- To start any process<br>
systemctl stop nginx/docker ---  To Stop any process<br>
journalctl -u nginx/docker ---- to show all logs of an individual process<br>

# User Management
whoami  ---- shoes which user is active<br>
sudo adduser xxx --- Adds user and made directory automatically <br>
sudo passwd xxx --- set up password for login<br>
su xxx --- command to enter inside user giving password (opens black bash)<br>
which bash --- which bash currently am i using (usually coloured) gives path<br>
sudo useradd -m yyy -s usr/bin/bash --- to make bash similar to **older coloured style** and using -m (Simialr to windows switching)<br>
cat /etc/group --- shows all the user group<br>
sudo addgroup ggg ---making group for user<br>
sudo gpasswd -a xxx ggg   ---adding user inside group. here xxx is added in group ggg along **with permission** gets added<br>
sudo gpasswd -d xxx ggg   ---To remove the user from that group and revoke their permissions. Restart with newgrp current user<br>
sudo usermod -aG docker ubuntu ---Adding an Ubuntu User to the docker Group to **avoid sudo** and have permissions<br>
sudo chown ggg filename.txt ---change the individual owner of the file from ubuntu to other user only valid for individual<br>
sudo chgrp xxx filename.txt --change group owner can be done with chown (:) as well<br>
# File System
Read (cat)<br>
Write (vim/nano)<br>
Execute (shell/ ./)<br>
mkdir -p devops  -----makes directory **with path** without error even if it exists do not throw error<br>
vim hello.txt > Insert i > write content > Esc > :wq(save and quit)/:q!(exit without saving)<br>
newgrp ubuntu --- changes current active primary group to the group named ubuntu for your current terminal session<br>
-rwxrwxrwx --read write execute for **owner group others** in sets of 3<br>
chmod 777 ---giving all permission / chmod 400 ----giving only read permission<br>
