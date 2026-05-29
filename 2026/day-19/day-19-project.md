# Task 1: Log Rotation Script
#!/bin/bash

log_rotate()
{
if [ $# -eq 0 ]; then
       echo " Enter the source path "
       exit 1
fi
       log="$1"
     count=$( find "$log" -name "*.log" -type f -mtime +7 | wc -l )

   find "$log" -name "*.log" -type f -mtime +7 -exec gzip {} +


   countd=$(find "$log" -name "*.gz" -type f -mtime +30 | wc -l)

   find "$log" -name "*.gz" -type f -mtime +30 -exec rm {} +

   echo "File Compressed : $count"
   echo "File deleted : $countd"
}
log_rotate "$1"

  # Task 2: Server Backup Script 
  #!/bin/bash

if [ $# -lt 2 ]; then
        echo " enter source and destination :"
fi

 src="$1"
 dest="$2"

 if [ ! -d "$src" ]; then
         echo "Source missing"
         exit 1
 fi

 mkdir -p "$dest"

 filename="backup_$(date +%Y-%m-%d).tar.gz"
 fullpath="$dest/$filename"

 tar -czf "$fullpath" "$src"

 if [ -f "$fullpath" ]; then
         echo "Backup created for $filename"
         echo "Size : $(du -h "$fullpath" | cut -f1)"

 find "$dest" -name "backup_*.tar.gz" -mtime +14 -exec rm {} +
 fi

# Task 3: Crontab(file timing is crutial min for min cron)
#!/bin/bash
set -euo pipefail

backup()
{
#1Hardcoded Paths
src="/home/ubuntu/devops-test"
dest="/home/ubuntu/devops"

mkdir -p "$dest"

#2 Crucial Time format so filenames change EVERY minute
filename="backup_$(date +%Y-%m-%d_%H%M).tar.gz"
fullpath="$dest/$filename"

#3 Create the archive
tar -czf "$fullpath" "$src"

#4 Print verification
if [ -f "$fullpath" ]; then
         echo "Backup created for $filename"
         echo "Size : $(du -h "$fullpath" | cut -f1)"

         # Clean up backups older than 14 days
         find "$dest" -name "backup_*.tar.gz" -mtime +14 -exec rm {} +
fi
}
backup

# Task 4: Combine — Scheduled Maintenance Script

#!/bin/bash

source /home/ubuntu/log_rotate.sh
source /home/ubuntu/backup.sh

 log="/var/log/maintenance.log"

 exce >> "$log" 2>&1

 #Print timestamped start banner
echo "=== Maintenance Started: $(date '+%Y-%m-%d %H:%M:%S') ==="

 echo "Rotation log"
 log_rotate "/home/ununtu/devops-test"

 echo "Backup"
 backup
 echo "=== Maintenance Completed: $(date '+%Y-%m-%d %H:%M:%S') ==="

Result:  sudo ./maintenance.sh /home/ubuntu/devops-test
File Compressed : 2
File deleted : 2
tar: Removing leading `/' from member names
Backup created for backup_2026-05-29_1203.tar.gz
Size : 12M
  
