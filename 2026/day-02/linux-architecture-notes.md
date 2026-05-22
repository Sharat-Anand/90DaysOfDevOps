# Devops Commad and systemd
A - Application/user<br>
S - Shell (terminal where you access shell)<br>
K -  Kernel<br>

BIOS runs Hardware ---> GNU GRUB load linux kernel ---> ubuntu loading --> init process/systemd<br> 

File System: / --root<br>
             / > ls ---you get bin sbin called directories binaries and systembinaries<br>
             /user/bin > ls --shows all the linux command<br>
             /user/you dir name -- make directory inside home and work here<br>
             
Everything start with process<br>
Command: uname -r ----Gives version of op system Kernel                           free ---shows memory <br>
         htop/top ---- all the process running                                    ip addr --gives ip address<br>
         ps aux | grep ping ----SS of running process                             systemctl start nginx/docker/python/ssh <br>
         ping XXXX.com ---gives all the ip of ping Api of website                 systemctl status docker/ssh<br>
         man <Command> (ex. man ls)  ----manuel for all the command<br>
         touch hello.txt --to make file<br>
         mkdir ---to make directory<br>
         ls -l --detail of file | ls cp in bin will show availablity<br>
         cp -r file1(source) file2(destination) --copy folder/files<br>
         mv file1(source) file2(destination) --rename/move files<br>
         rmdir filename/ rm -r filename ---to remove directory(shift delete similar for rm command)<br>
