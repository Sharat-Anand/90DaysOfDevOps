# Task 1: Log Rotation Script
#!/bin/bash

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


src="/home/ubuntu/devops-test"
dest="/home/ubuntu/devops"

mkdir -p "$dest"

#Crucial Time format so filenames change EVERY minute
filename="backup_$(date +%Y-%m-%d_%H%M).tar.gz"
fullpath="$dest/$filename"


tar -czf "$fullpath" "$src"

# 4. Print verification
if [ -f "$fullpath" ]; then
         echo "Backup created for $filename"
         echo "Size : $(du -h "$fullpath" | cut -f1)"

         # Clean up backups older than 14 days
         find "$dest" -name "backup_*.tar.gz" -mtime +14 -exec rm {} +
fi
