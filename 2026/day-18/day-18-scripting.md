# Task 1
#!/bin/bash

greet()
{
  echo "hello $1 !!!"
}

add()
{
  echo "The sume of 2 numbers $1 and $2 is :"
  local a=$1
  local b=$2
  local sum=$(( a + b ))
  echo "$sum"
}

greet "$1"
add "$2" "$3"

# Task 2: Functions with Return Values
#!/bin/bash

check_disk()
{
         echo " currect working directory"
         pwd
         echo "$pwd"
         echo "Going to root directory..."
         cd / && df -h

}

check_memory()
{
         echo " currect working directory"
         pwd && echo "$pwd"
         echo "Going to root directory..."
         cd / && free -h

}

check_disk
check_memory

# Task 3: Strict Mode — set -euo pipefail
#!/bin/bash

set -euo pipefail

echo "=== STAGE 1: Testing 'set -u' (Undefined Variables) ==="
echo "$name is sharat"     

echo "=== STAGE 2: Testing 'set -e' (Failing Commands) ==="
commamd
echo "Command is a fake command"

echo "=== STAGE 3: Testing 'set -o pipefail' (Piped Failures) ==="
command | grep --color=never "anything"

Results :  ./strict_demo.sh: line 6: name: unbound variable
           ./strict_demo.sh: line 9: commamd: command not found
           ./strict_demo.sh: line 13: anything: command not found

# Task 4 Local Variables
#!/bin/bash

safe()
{
  local a="password"
  echo "$a is safe"
}

leak()
{
   b="pass"
   echo "$b"
}

echo"$a"
safe

leak
echo "may be leaked value $b "

 Result : password is safe
          pass
          may be leaked value pass

# Task 5 Build a Script — System Info Reporter
#!/bin/bash
set -euo pipefail
host()
{
         echo "OS Details"
         source /etc/os-release && echo "$PRETTY_NAME"
         echo " Hostname : $(hostname) "

}

time_up()
{
    uptime -p
}

disk_use()
{
   df -h --output=source,size | head -n 5
}

mem()
{
    ps -o pid,pmem,comm  --sort=-pmem |head -n 5
}
main()
{
        host
        time_up
        disk_use
        mem
}
main

Result :
OS Details
Ubuntu 26.04 LTS
 Hostname : ip-172-31-43-101
up 6 hours, 11 minutes
Filesystem       Size
/dev/root        6.7G
tmpfs            455M
tmpfs            182M
efivarfs         128K
    PID %MEM COMMAND
  16945  1.3 vim
  23108  0.7 head
  10415  0.6 bash
  23107  0.4 ps
