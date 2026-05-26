# Task 1
vim hello.sh 
ls -l hello.sh
chmod 775 hello.sh
./hello.sh
Without shebang it displays the same result.

# Task 2

#!/bin/bash
NAME=Sharat
ROLE=DevopsEngineer
echo "Hello, I am $NAME and I am $ROLE"
echo 'Hello, I am $NAME and I am $ROLE'

# Task 3
vim greet.sh
#!/bin/bash
read -p "Enter your name :" Name
read -p "enter you favourite tool :" Tool
echo "Hello $Name your favourite tool is $Tool"       

# Task 4

#!/bin/bash
read -p "Enter a number: " Number
if [ $Number -gt 0 ];then
       echo " $Number is positive"
elif [ $Number -lt 0 ];then\
        echo "$Number is negative"
else    echo "The number is zero"
fi

#!/bin/bash
read -p "Enter the filename :" Filename
if [ -f $Filename ]; then
        echo "$Filename already exist"
else
        echo " Your $Filename dosenot exist"
fi

# Task 5

#!/bin/bash
Servicename="nginx"
read -p "Do you want to check service status for $Servicename. Enter Y or N :" Enter
if [[ $Enter == 'Y' ]]; then
        echo "Checking status for $Servicename ...."
        systemctl status "$Servicename" --no-pager
        if systemctl  is-active "$Servicename"; then
                echo "$Servicename is running"
        else
                echo "$Service is not active"
                fi
else
        echo " Thanks for the $Servicename exploration!!"
fi
