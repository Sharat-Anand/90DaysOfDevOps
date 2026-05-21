Systemctl status ssh/docker  --- to see the curreent status of a single process<br>
<img width="941" height="132" alt="image" src="https://github.com/user-attachments/assets/a753e730-bd4e-4edc-90e3-bb630f2359da" />

sudo systemctl start  nginx/docker/ssh ----to stop the process <br>
<img width="970" height="110" alt="image" src="https://github.com/user-attachments/assets/06be6f0b-e541-46d4-96ee-379b89a0044b" />

sudo systemctl stop  nginx/docker/ssh ----to stop the process<br>
<img width="971" height="157" alt="image" src="https://github.com/user-attachments/assets/eec3aa2d-1fea-4b8f-bb2f-2ac99a5aa238" />

ping zeiss.com ---Sends icmp packets to the hosts<br>
htop -- to see the running status of the process and track live running process<br>
<img width="1022" height="522" alt="image" src="https://github.com/user-attachments/assets/107a7da9-5eb9-4448-bb0d-cb702a94fa55" />

ps aux | grep zeiss --it create the screen shot of the process and grep filter the required process<br>
kill -9 PID --force kill the running process<br>
kill PID --kill the process<br>
<img width="1086" height="205" alt="image" src="https://github.com/user-attachments/assets/1d504474-630b-401e-9678-a9134758541d" />

systemctl list-units ----command displays all currently loaded and active \(systemd\) units (like services, sockets, and mount points) in memory.<br>
systemctl list-units --state=failed<br>
systemctl list-units --state=waiting<br>
<img width="1342" height="187" alt="image" src="https://github.com/user-attachments/assets/2611afdc-3add-4d46-ae22-d1535ef20661" />

journalctl -u docker/nginx/ssh --- to see all the log file of a sinle process<br>
<img width="1447" height="92" alt="image" src="https://github.com/user-attachments/assets/59708455-c1e3-4761-9adc-7ceb5abc13f0" />

head -n 5 <file name> --- this is to see first 5 line in log files or any files<br>
<img width="1447" height="230" alt="image" src="https://github.com/user-attachments/assets/aa441a6c-cc10-4399-a00e-227c567e6d3d" />

tail -n 5 <file name> --- this is to see last 5 line in log files or any files<br>
<img width="1446" height="207" alt="image" src="https://github.com/user-attachments/assets/3b260983-9870-4fe7-9afc-c69db584635f" />

# Process additional command
pstree ubuntu --- Visualizes running processes in a hierarchical, parent-child tree structure<br>
pgrep nginx  --- Searches for processes by name and returns their Process IDs (PIDs) <br>
<img width="487" height="341" alt="image" src="https://github.com/user-attachments/assets/977cafe5-2d1d-4f4c-bf6c-aca0c5c3718c" />
