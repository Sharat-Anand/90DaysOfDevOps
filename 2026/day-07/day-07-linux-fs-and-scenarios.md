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

