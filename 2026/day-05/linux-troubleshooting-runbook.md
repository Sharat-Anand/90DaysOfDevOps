# Environment Basic
uname -a  --give details aboutabout the Linux kernel and hardware architecture (What it outputs: Kernel version, kernel build date, CPU architecture)<br>
lsb_release -a (The Legacy Standard) --- prints all available Linux Standard Base (LSB) and **distribution-specific** version details<br>
cat /etc/os-release (The Modern Standard) --- tells you about the specific **Linux distribution** (OS) and its version<br>
<img width="1262" height="527" alt="image" src="https://github.com/user-attachments/assets/2ac70fb0-bec5-4c8d-abed-2fe8a4c174fe" />

# filesystem sanity
mkdir /tmp/runbook-demo  ---make directory<br>
cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo --copy directory file from hosts to copy hosts and dispalys permission<br>
<img width="1157" height="112" alt="image" src="https://github.com/user-attachments/assets/ef507f8c-4b97-4786-82d4-1069b710bf26" />

# Troubleshooting
systemctl status docker --- one target service/process to see the status<br>
<img width="1047" height="116" alt="image" src="https://github.com/user-attachments/assets/597b3818-588f-419b-b3eb-691cc1c53e5c" />

htop --to see the running process
<img width="1338" height="126" alt="image" src="https://github.com/user-attachments/assets/cb02c30d-793a-490b-ac12-b44487bb3595" />
<img width="1640" height="163" alt="image" src="https://github.com/user-attachments/assets/740b5135-7c23-4aff-891e-2646d713df01" />

 # customized details of CPU / Memory <br>
ps -o pid,pcpu,pmem,comm -p <pid> --- ps is process -o user-defined format pid - unique process id<br>
            pcpu --- details about cpu                     pmem --- detail about memory<br>
            comm ---  short executable command -p <pid>--- specific process ID<br>
 free -h  --- shows free space in human redeable format. without -h it is in byte format<br>
<img width="982" height="276" alt="image" src="https://github.com/user-attachments/assets/357d0c1c-e675-4a8d-bb26-aaa64ecf84b3" />

# Disk / IO
df -h --detail of file system mounted<br>
du -sh /var/log --- calculates and displays the total disk space used by the /var/log folder in redeable format number<br>
iostat --- Focuses heavily on storage drive performance and input/output (I/O) speeds and idle time<br>
vmstat --- Focuses heavily on virtual memory, RAM, paging, processes, and CPU activity(Virtual Memory Statistics)<br>
dstat --- Combines both tools into a single, Everything simultaneously—CPU, disk, network, and memory(Versatile Statistics)<br>
<img width="1165" height="957" alt="image" src="https://github.com/user-attachments/assets/486b7db3-9bcb-450d-b4a8-50e4229b7eb8" />

# Network
ss -tulpn -- display all open and listening network ports<br>
<img width="1241" height="227" alt="image" src="https://github.com/user-attachments/assets/0e9bdab3-aeb7-4836-a5e7-e7870b742d85" />

netstat -tulpn  ---  displays same data but its old style <br>
<img width="1162" height="163" alt="image" src="https://github.com/user-attachments/assets/2b8c9bee-d9ae-4202-a389-b53876e4099f" />

ping zeiss.com --checks network connectivity at the system level using ICMP (Is the server powered on and reachable?)<br>
curl -I  API     ---- checks application-layer web responses using HTTP(give full address) (Is the web application/API running and healthy?)<br>
<img width="953" height="302" alt="image" src="https://github.com/user-attachments/assets/e850a2ef-eade-48a9-b0e8-d16666cd19a4" />

# Logfile
journalctl -u docker -n 5 ---shows the detail of any running process depending on number of lines asked (here 5 lines of docker)<br>
tail -n 5 /var/log/syslog  --- last 5 lines of a particular log files <br>
<img width="1451" height="348" alt="image" src="https://github.com/user-attachments/assets/4ef3ee13-4ab1-4129-a2cf-2988d1102e30" />

# If this worsens(example Nginx)
Nginx Troubleshooting ChecklistFollow this sequential checklist to diagnose, configure, and isolate web server failures<br>
Phase 1: Initial Triage & VerificationVerify OS Environment: Run cat /etc/os-release to confirm the distribution baseline.<br>
Test Network Reachability: Run ping <target-ip> to verify the physical server is online.<br>
Inspect HTTP Headers: Run curl -I http://localhost to capture the exact status code (e.g., 502 Bad Gateway).<br>
Audit Open Ports: Run sudo ss -tulpn to ensure Nginx is actively listening on ports 80/443.

Phase 2: Elevate Verbosity (The "If This Worsens" Plan)<br>
Open Configuration: Run sudo nano /etc/nginx/nginx.conf (Do not use cd).
Enable Debug Logs: Locate the error_log directive and append debug to the end of the line:**nginxerror_log /var/log/nginx/error.log debug**<br>
Test Layout Syntax: sudo nginx -t ---- to verify there are no missing semicolons or typos.<br>
Apply Changes Safely: sudo systemctl reload nginx --- to load the settings without dropping user traffic.<br>
Stream Live Errors: sudo tail -f /var/log/nginx/error.log --- to watch the debug output in real time.

Phase 3: Advanced Diagnostics & RecoveryTrace System Calls: Run sudo strace -fp <PID> -e trace=network,file on a worker PID if the process hangs.Isolate and Restart: If the state corrupts, run sudo systemctl stop nginx, confirm ports are vacant with ss, then run sudo systemctl start nginx.


