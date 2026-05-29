# Task 1: Input and Validation
#!/bin/bash

#Exit immediately if a command fails (-e) or an unset variable is used (-u)
set -euo pipefail

#1. Check if the user forgot to provide a file path argument
if [ $# -eq 0 ]; then
    echo "ERROR: No log file path provided." >&2
    echo "Usage: $0 <path_to_log_file>" >&2
    exit 1
fi
log="$1"
if [ ! -f "$log" ];then
        echo "ERROR: File '$log' does not exist." >&2
        exit 1
fi
echo "Success: File '$log' found and ready for analysis."

Result: ./log_analyzer.sh /var/log/maintenance.log
Success: File '/var/log/maintenance.log' found and ready for analysis.

# Task 2: Error Count(cont..of task1 code)

 err=$(grep -E "ERROR|Failed" "$log" | wc -l || true)

    echo "Total number of lines : $err "
    
Result : ./log_analyzer.sh /var/log/maintenance.log
Success: File '/var/log/maintenance.log' found and ready for analysis.
Total number of lines : 4

 # Task 3: Critical Events( cont... task1)
 
grep -n "CRITICAL" "$log" | awk -F':' '{print "Line " $1 ": " $2}' || true

REsult :  ./log_analyzer.sh /var/log/maintenance.log
======TASK 3=============
Line8:2026-05-29 14
Line9:2026-05-29 14

# Task 4: Top Error Messages( cont... task1)
 echo "======TASK 4============="
 grep -E "ERROR" "$log" | sed -E 's/^[0-9]{4}-[0-9]{2}-[0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2} //'  | sort | uniq -c | sort -rn |head -5 ||true

# Task 5: Summary Report

      echo "=====TASK 5========"

   curdate=$(date +%Y-%m-%d)
   logfile="log_report_${curdate}.txt"
   LOG_FILENAME=$(basename "$log")

   totline=$(wc -l < "$log" )

   # FIX 1: Added -Ei for case matching and pointed it to "$log" file
   errline=$(grep -Ei "ERROR|Failed" "$log" | wc -l || true)

   # FIX 2: Corrected the target search pattern to "ERROR" and added "$log" file
   toperr=$(grep -E "ERROR" "$log" | sed -E 's/^[0-9]{4}-[0-9]{2}-[0-9]{2} [0-9]{2}:[0-9]{2}:[0-9]{2} //' | sort | uniq -c | sort -rn | head -5 || true)

   # FIX 3: Extracted critical events cleanly to populate the report variable
   CRITICAL_EVENTS=$(grep -n "CRITICAL" "$log" | awk -F':' '{print "Line " $1 ": " $2}' || true)

   {
    echo "=================================================="
    echo "               DAILY LOG SUMMARY REPORT           "
    echo "=================================================="
    echo "Date of Analysis:     $curdate"
    echo "Log File Name:        $LOG_FILENAME"
    echo "Total Lines Processed: $totline"
    echo "Total Error Count:    $errline"
    echo "--------------------------------------------------"
    echo "Top 5 Error Messages:"
    if [ -z "$toperr" ]; then
        echo "None detected."
    else
        echo "$toperr"
    fi
    echo "--------------------------------------------------"
    echo "Critical Events:"
    if [ -z "$CRITICAL_EVENTS" ]; then
        echo "None detected."
    else
        echo "$CRITICAL_EVENTS"
    fi
    echo "=================================================="
} > "$logfile"

echo -e "\n[INFO] Summary report successfully generated: $logfile"
