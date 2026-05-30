# Task 1: Basics
1.Shebang (#!/bin/bash) — Its says kernal what type of content is present<br>
2.Running a script : chmod +x ---gives permission(rwx) ,
 ./script.sh --cmd to execute  bash script.sh---ignore shebang force execution using bash<br>
3.Comments — single line (#) and inline---- singel line comment <br>
4.Variables — declaring, using, and quoting ($VAR, "$VAR", '$VAR')
5.declearing variable using $VAR , using same variable "$VAR" , '$VAR' traeating character as literals strings not variable<br>
6.Reading user input —---read -p "Enter..." VAR : This is way to call from user<br>
7.Command-line arguments — $0(usually file name), $1(First arg), $#(Number of Arg), $@(dispaly all arg entered by user), $?(exit status of the last executed command)<br>

# Task 2: Operators and Conditionals
1.String comparisons — = strings are equal, != strings are not equal, -z true if string is empty, -n true when string is non empty<br>
2.Integer comparisons — -eq(equal to), -ne(notn equal to), -lt(les than), -gt(greater than), -le(less than), -ge(greater then equals)<br>
3.File test operators — -f (true for file), -d(true for directory), -e(true for path), -r(gives read), -w (gives write), -x(execute), -s (file exist)<br>
4.if []; then, elif []; then, else syntax---of else if
5.Logical operators — && (both are true), ||(one is true), !(logical not)
6.Case statements — case ... esac : cases

# Task 3: Loops
Document with examples:
1. `for` loop — list-based and C-style
   
   #Iterating over explicit items
for color in Red Green Blue; do
    echo "Color: $color"
done

#Iterating over a number range {start..end..step}
for i in {1..5..2}; do
    echo "Number: $i"
done

#C Style
for ((i=1; i<=3; i++)); do
    echo "Count: $i"
done

2. `while` loop
    count=1
while [ $count -le 3 ]; do
    echo "Value: $count"
    ((count++)) # Increment the variable
done

3. `until` loop
   count=1
until [ $count -gt 3 ]; do
    echo "Value: $count"
    ((count++))
done

4. Loop control — `break`, `continue`
   for num in {1..5}; do
    if [ $num -eq 2 ]; then
        continue # Skip the rest of the code for number 2
    fi
    if [ $num -eq 5 ]; then
        break # Exit the loop completely when reaching 5
    fi
    echo "Number: $num"
done
   
5. Looping over files — `for file in *.log`
   #Process all log files in the current directory
for file in *.log; do
    #Check if files actually exist to avoid running on literal '*.log'
    if [ -f "$file" ]; then
        echo "Processing file: $file"
    fi
done
  
6. Looping over command output — `while read line`
   
   #Reading line-by-line from a command pipeline
df -h | while read -r line; do
    echo "Disk info: $line"
done

#Reading line-by-line directly from a file
while read -r line; do
    echo "Line content: $line"
done < input.txt

# Task 4: Functions
1. Defining a function — function_name() { ... }
   #Definition
show_welcome() {
    echo "Welcome to the system automation script!"
}

2. Calling a function
   #Call the function defined above
   show_welcome

3. Passing arguments to functions — $1, $2 inside functions
   #Define a function that expects two inputs
show_user_info() {
    echo "The username is: $1"
    echo "The assigned role is: $2"
}

#Call the function and pass two string arguments
show_user_info "admin_user" "System Administrator"

4. Return values — return vs echo
#Method 1: Using 'return' for success/failure checks
check_root() {
    if [ "$USER" = "root" ]; then
        return 0 # Success
    else
        return 1 # Error/Failure
    fi
}

#Method 2: Using 'echo' to send back actual data strings
calculate_tax() {
    local total=$(($1 * 2))
    echo "$total"
}

#Running Method 1
check_root
echo "Exit status was: $?"

#Running Method 2 (Capturing output into a variable)
final_bill=$(calculate_tax 50)
echo "The calculated tax amount is: $final_bill"

5. Local variables — local
   #!/bin/bash

#A global variable
CITY="Berlin"

update_location() {
    # Local variable: only exists inside this function
    local CITY="Paris"
    echo "Inside function, CITY is: $CITY"
}

#Run the function
update_location

#Check global variable value
echo "Outside function, CITY is still: $CITY"

Result:
Inside function, CITY is: Paris
Outside function, CITY is still: Berlin

# Task 5: Text Processing Commands

1. grep — Search PatternsUsed to search text files for lines matching a specified pattern.<br>
-i: Ignores character case (matches both error and ERROR).<br>
-r: Recursively searches all files inside directories and subdirectories.<br>
-c: Displays only the numerical count of matching lines instead of the text.<br>
-n: Displays the line number in the file where the match was found.<br>
-v: Inverts the match, printing only lines that do not match the pattern.<br>
-E: Enables Extended Regular Expressions (ERE) for complex patterns using | or ?.<br>

2. awk — Field Processing and Patterns
1, $2, $NF: Represents column numbers.<br>
$NF automatically references the very last column.<br>
-F: Defines a custom field separator character (defaults to whitespace).<br>
BEGIN { ... }: Executes commands before any text rows are processed.<br>
END { ... }: Executes commands after all text rows have been processed.<br>

Example :
#Print the 1st and 3rd columns from a colon-separated file (like /etc/passwd)
awk -F':' '{print $1, $3}' /etc/passwd

#Print lines where the 3rd column value is greater than 100
awk '$3 > 100 {print $0}' data.txt

3. sed — Stream Editor
s/search/replace/g: Substitutes 'search' with 'replace' globally across the line.<br>
d: Deletes targeted lines matching a pattern or line number.<br>
-i: Edits the file in-place directly instead of printing output to the terminal screen.<br>

Example :
#Replace 'http' with 'https' globally in a file and save changes directly
sed -i 's/http/https/g' config.txt

#Delete line 5 from a text file
sed '5d' data.txt

4. cut — Extract Columns
 -d: Sets the custom delimiter character (must be a single character).<br>
-f: Specifies which fields/columns to extract (e.g., -f1 or -f2,4).<br>
-c: Extracts specific character positions or ranges instead of columns.<br>  

Example :
#Extract the 1st and 2nd columns from a comma-separated CSV file
cut -d',' -f1,2 addresses.csv

5. sort — Arrange Lines
-n: Sorts values numerically rather than treating them as standard string text.<br>
-r: Reverses the sorted output order (e.g., descending instead of ascending).<br>
-u: Outputs only unique matching rows, throwing away exact duplicates.<br>

Example :
#Sort log file numbers numerically in reverse order
sort -nr prices.txt

6. uniq — Deduplicate and CountFilters or displays duplicate lines from an input source. Note: uniq only detects adjacent duplicate lines, so you must run sort before it.<br>
-c: Prefixes each unique line with the total number of times it occurred.
-u: Prints only unique lines that never repeat in the file.
-d: Prints only lines that have matching duplicate copies.

Example :
#Find unique lines and count their occurrences
sort names.txt | uniq -c

7. tr — Translate or Delete Characters
   Transforms, squeezes, or deletes characters from standard input. It does not accept filenames directly as arguments.
   -d: Deletes specified target characters from the input text stream entirely.<br>
   -s: Squeezes repeating identical characters down to a single character instance.<br>

Example:
#Convert all lowercase text to uppercase characters
echo "hello world" | tr 'a-z' 'A-Z'

#Delete all carriage return characters (\r) from a Windows text file
tr -d '\r' < windows.txt > linux.txt

8. wc — Word CountCalculates counts for lines, words, and characters inside data.<br>
   -l: Displays the total line count.-w: Displays the total word count.<br>
   -c: Displays the total byte/character count.<br>

   Example :
   #Count how many total lines are present inside a log file
   wc -l system.log
   
10. head / tail — File InspectionDisplays portions from the beginning or absolute end of text files.<br>
   -n X: Limits output to exactly X lines (e.g., -n 5 or -n 20).<br>
   -f: (Tail only) Enters continuous follow mode, printing new log lines onto the screen in real-time as they are written.<br>

   Example :
   #View the first 5 lines of a configuration file
   head -n 5 setup.conf

   #Watch a system log update in real-time as events occur
   tail -f /var/log/syslog

# Task 6: Useful Patterns and One-Liners

1. Find and Delete Files Older Than 30 Days
   
   find /var/log/app/ -type f -name "*.log" -mtime +30 -delete

2. Track Top 5 Error Sources in Real Time (Tail + Filter)

  tail -f /var/log/syslog | grep --line-buffered -i "error" | awk '{print $5, $6}'

3. Replace a String Across Multiple Files In-Place

   grep -rl "http://old-api.local" ./src/ | xargs sed -i 's|http://old-api.local|https://production.com|g'

4. Check if a Service is Running (With Action)

   systemctl is-active --quiet nginx || (echo "Nginx down! Restarting..." && systemctl start nginx)

5. Aggregate and Count HTTP Status Codes from a Log

   awk '{print $9}' /var/log/nginx/access.log | sort | uniq -c | sort -nr

# Task 7 : Error Handling and Debugging

1. Exit Codes — $?, exit 0, exit 1
   exit 0: Terminates the script and signals absolute success.
   exit 1 (or any value up to 255): Terminates the script and signals a specific error.

   Example :
   #!/bin/bash

TARGET_FILE="/etc/missing_config.conf"

if [ ! -f "$TARGET_FILE" ]; then
    echo "Critical Error: Configuration file missing!"
    exit 1 # Stops script immediately, returns status 1
fi

echo "File found."
exit 0 # Script finished successfully

2. set -e — Exit on Error

#!/bin/bash
set -e

#If this directory does not exist, the script stops right here
cd /non/existent/directory 

#This line will never execute because of 'set -e'
echo "This message will not print." 

3. set -u — Treat Unset Variables as Error
   
#!/bin/bash
set -u

USER_NAME="Alice"

#Typo in variable name throws an error and crashes the script safely
echo "Welcome, $USER_NAM" 

4.  set -o pipefail — Catch Errors in Pipes
  
  #!/bin/bash
#Without pipefail, this entire line returns 0 (success) because wc succeeds
#With pipefail, this line returns a non-zero failure because cat fails
set -o pipefail

cat non_existent_file.txt | wc -l
echo "Pipeline exit status: $?"

5. set -x — Debug Mode (Trace Execution) ---Prints every command to the terminal screen exactly as it gets executed, with variables fully expanded. 

 #!/bin/bash

#Turn on debugging trace
set -x 

PREFX="Backup"
DATE=$(date +%F)
FILENAME="${PREFX}_${DATE}.tar.gz"

#Turn off debugging trace
set +x 

echo "Generated: $FILENAME"

Result : 
+ PREFX=Backup
++ date +%F
+ DATE=2026-05-31
+ FILENAME=Backup_2026-05-31.tar.gz
+ set +x
Generated: Backup_2026-05-31.tar.gz

6. Trap — trap 'cleanup' EXIT ---Allows you to intercept system signals or script termination.
   
#!/bin/bash
set -e

#Define a cleanup function
cleanup_temp_files() {
    echo "Cleaning up temp directory..."
    rm -rf "$TEMP_DIR"
}

#Register the trap: Run the function whenever the script exits
trap cleanup_temp_files EXIT

#Create a temporary working workspace
TEMP_DIR=$(mktemp -d)
echo "Working in: $TEMP_DIR"

#Simulate a script failure
ls /invalid/folder/path

Result :
 Working in: /tmp/tmp.jK98dx2Z
ls: cannot access '/invalid/folder/path': No such file or directory
Cleaning up temp directory...
