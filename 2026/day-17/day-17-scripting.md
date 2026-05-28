# Task 1 For Loop
Loop of 5 fruits
#!/bin/bash

echo "list of fruits are :"

for i in {apple,mango,banana,grapes,kiwi}
do
        echo "$i"
done

----------------Loop of number 1to 10
#!/bin/bash

echo "the numbers between 1 to 10 :"

for (( i = 1; i<=10; i++ ))
do
        echo "$i"
done

# Task 2 While Loop

#!/bin/bash
read -p "Enter the numbers :" num

echo "Number in reverse order are"
while (( num > 0 ))
do
        echo "$num"
        (( num-- ))
done

# Task 3 Arguments with $ signs
#!/bin/bash


if [ -z "$1" ];then
        echo "Usage: ./greet.sh"
        exit 1
else

        echo "Hello $1 !!"
fi

----demo arguments
#!/bin/bash

echo " total number of arguments entered : $#"

echo " all the arguments are $@"

echo " the script name is : $0"

# Task 4 Pakagae_Installation
#!/bin/bash

for i in nginx curl wget
do
        if  dpkg -s "$i" >/dev/null 2>&1; then
                echo "Pakage already exists ..."
        else
                echo "Installing pkg ...."
                sudo apt-get update && sudo apt-get install -y "$i"
        fi
done

# Task 5 Error_Handling
#!/bin/bash

set -e

mkdir  /home/ubuntu/devops-test || echo "Directory already exist"

echo "Navigating inside directory .../home/ubuntu/devops-test"
cd /home/ubuntu/devops-test
echo "creating file inside new directory.."
touch file.txt
