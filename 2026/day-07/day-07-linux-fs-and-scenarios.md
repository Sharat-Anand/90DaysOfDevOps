# Linux File System Hierarchy
Symbol / --root consists of all folder. System starts from here<br>
 / > ls -l ---you get bin sbin called directories binaries and system binaries<br>
 /user/bin > ls --shows all the linux command<br>
 /bin ---  Essential command binaries all the commands are either on bin and system command is in sbin<br>
 /user/<your directory> -- make directory inside home and work here<br>
 /opt --- Optional/third-party applications<br>

  /var/log - **Log files** -- all log files and can open through vim<br>
 <img width="550" height="232" alt="image" src="https://github.com/user-attachments/assets/96317d6a-93e9-4b40-a81f-1ba441353b4f" />

du -sh /var/log/*  2>/dev/null -- du -sh --is disk space -sh flah is summerize and human readable the log file, *wildcard to trace all<br>
                               -- 2>dev/null ---its a black hole where all eoor goes for example permission denied

 Find the largest log file in /var/log. Use of log file scenario
du -sh /var/log/*  2>/dev/null | sort -h | tail -n 5 --sort and gives result of last 5 files<br>
<img width="692" height="132" alt="image" src="https://github.com/user-attachments/assets/f7ce3f71-7c07-4b96-912a-d0c6d0a6b0a6" />

Negative scenarios --- this is without blackhole(**2>/dev/null**)<br>
<img width="588" height="187" alt="image" src="https://github.com/user-attachments/assets/91c0cfa2-09f1-43a2-9b2c-dc3e88048604" />

Look at a config file in /etc --shows which host is aasigned<br>
cat /etc/hostname  ---displays the unique network name assigned to your Linux system<br>

Check your home directory
ls -la ~ ---list aal hidden file but ~ is used to access home directory from anywhere

# Scenario 1
  systemctl status myapp  ----Check the status of myapp<br>
  systemctl is-enabled myapp  --is system enabled<br>
  sudo journalid -u myapp -e --no-pager   --check the log file in chronological order<br>
  sudo ss -tulpn -- Check other service (like Apache or Nginx) already grabbed the port myapp needs<br>

 # Scenario 2
 htop --to see memory usage
 ps aux --sort=-pcpu | head -n 5 -- (-pcpu) arrange in decending and apply head or remove minus and apply tail<br>

  # Scenario 3
  systemctl status docker  ---status of docker <br>
  journalctl -u docker -n 50 ---chek log file<br>
  journalctl -u docker -f --follow log in real time<br>

  # Scenario 4
 ls -l home/user/backup.sh --to check the permission<br>
 chmod a+x home/user/backup.sh --gives permission to execute to all<br>
 ls -l home/user/backup.sh  --verify all cmd  has r-xr-xr-x permission<br>
 (or) chmod 755 will work --based on number system but it has all the group<br>

  
