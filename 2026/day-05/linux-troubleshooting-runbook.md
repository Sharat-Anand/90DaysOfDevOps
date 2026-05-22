# Troubleshooting
systemctl status docker --- one target service/process to see the status<br>
<img width="1047" height="116" alt="image" src="https://github.com/user-attachments/assets/597b3818-588f-419b-b3eb-691cc1c53e5c" />

htop --to see the running process
<img width="1338" height="126" alt="image" src="https://github.com/user-attachments/assets/cb02c30d-793a-490b-ac12-b44487bb3595" />
<img width="1640" height="163" alt="image" src="https://github.com/user-attachments/assets/740b5135-7c23-4aff-891e-2646d713df01" />

 # customized details of CPU / Memory <br>
ps -o pid,pcpu,pmem,comm -p <pid> --- ps is process -o user-defined format pid - unique process id<br>
                                      pcpu --- details about cpu pmem --- detail about memory<br>
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
