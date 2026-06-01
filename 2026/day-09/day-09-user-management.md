# Task 1: Create Users
sudo adduser professor (password & details automatically asked)<br>
sudo adduser tokyo <br>
sudo useradd -m berlin -s usr/bin/bash ---craeteonly user name <br>
sudo passwd berlin ---to create password

# Task 2: Create Groups
Create group named developers   ----sudo addgroup developers
Create group named admins --- sudo addgroup admins

# Task 3: Assign to Groups
sudo usermod -aG developers tokyo         --tokyo → developers<br>
sudo usermod -aG developers,admins berlin ---berlin → developers + admins (both groups)<br>
sudo gpasswd -a professor admins         --- professor → admins<br>
Check group after each step              ---  cat /etc/group<br>

# Task 4: Shared Directory
sudo mkdir -p /opt/dev-project   ---Create directory: /opt/dev-project<br>
sudo chown :developers /opt/dev-project ----change owner to developer<br>
sudo chmod 775 /opt/dev-project/   --chnage permission<br>
<img width="593" height="135" alt="image" src="https://github.com/user-attachments/assets/f7352af6-6cf8-49b7-aa8e-5f6be2854b4c" />

cd /opt/dev-project >>> su berlin --file created inside<br>
berlin@ip-172-31-43-101:/opt/dev-project$ touch berlin.txt  --creates file<br> 

cd /opt/dev-project >>> su tokyo --file created inside<br>
tokyo@ip-172-31-43-101:/opt/dev-project$ touch tokyo.txt<br>

#Testing negative scenario
This happened because owner is changed to developer so dev has tokyo and berlin added not professor
cd /opt/dev-project >>> su professor  user enters<br>
<img width="615" height="132" alt="image" src="https://github.com/user-attachments/assets/e89067ce-6dbb-4bee-baab-2cee95fa02ec" />

# Task 5: Team Workspace
sudo addgroup project-team --Create user nairobi with home directory<br>
sudo usermod -aG project-team niarobi<br>
sudo usermod -aG project-team tokyo<br>
<img width="607" height="400" alt="image" src="https://github.com/user-attachments/assets/1a6a9de3-5df2-4ef2-a1ce-f461927bc653" />

sudo mkdir -p /opt/team-workspace ---Create /opt/team-workspace directory<br>
<img width="551" height="120" alt="image" src="https://github.com/user-attachments/assets/212e88c0-4972-49cc-93f3-18ea03584f85" />

sudo chmod 775 /opt/team-workspace/ ---Set group to project-team, permissions to 775<br>
Test by creating file as nairobi <br>
<img width="567" height="115" alt="image" src="https://github.com/user-attachments/assets/1335d741-09dc-46c5-aea9-b75dbe589196" />

Learning :(both commands are simialr)
sudo chown :project-team ubuntu 
sudo chgrp project-team ubuntu
