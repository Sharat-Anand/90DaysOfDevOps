# Part 1: Launch Cloud Instance & SSH Access
Step 1: Create a Cloud Instance<br>
Step 2: Connect via SSH<br>

# Part 2: Install Docker & Nginx
 Step 1: Update System ---  sudo apt update<br>
 Step 3: Install Nginx  --  sudo apt-get install nginx<br>
 Verify Nginx is running: -- systemctl status nginx<br>

 # Part 3: Security Group Configuration
 http://51.21.160.162/
 <img width="1227" height="377" alt="image" src="https://github.com/user-attachments/assets/27aa8f74-701c-4664-8ea4-ad1654737b36" />

# Part 4: Extract Nginx Logs
Step 1: View Nginx Logs --- cd /var/log/nginx<br>
                            tail -f /var/log/nginx/access.log<br>
Step 2: Save Logs to File(~ home) --- cp -r error.log ~/nginx.txt<br> 
Step 3: Download Log File to Your Local Machine --- scp -i shell-scripting.pem ubuntu@51.21.160.162:~/nginx.txt .<br>
