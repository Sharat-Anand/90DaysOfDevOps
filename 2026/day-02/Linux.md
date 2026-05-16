# Devops Commad and systemd
A - Application/user
S - Shell (terminal where you access shell)
K -  Kernel

BIOS runs Hardware ---> GNU GRUB load linux kernel ---> ubuntu loading --> init process/systemd 

File System: / --root
             / > ls ---you get bin sbin called directories binaries and systembinaries
             /user/bin > ls --shows all the linux command
             /user/you dir name -- make directory inside home and work here
             
Everything start with process
Command: uname -r ----Gives version of op system Kernel                           free ---shows memory
         htop/top ---- all the process running                                    ip addr --gives ip address
         ps aux | grep ping ----SS of running process                             systemctl start nginx/docker/python/ssh
         ping XXXX.com ---gives all the ip of ping Api of website                 systemctl status docker/ssh
         man <Command> (ex. man ls)  ----manuel for all the command
         touch hello.txt --to make file
         mkdir ---to make directory
         ls -l --detail of file | ls cp in bin will show availablity
         cp -r file1(source) file2(destination) --copy folder/files
         mv file1(source) file2(destination) --rename/move files
         rmdir filename/ rm -r filename ---to remove directory(shift delete similar for rm command)
