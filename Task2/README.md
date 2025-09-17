# Task 2: User Management and Access Control

# Create User Accounts

Add users Sarah and Mike with home directories:
sudo useradd -m Sarah
sudo useradd -m mike

Set passwords (input strong passwords):
sudo passwd Sarah
sudo passwd mike

**Note: Taken screenshots of setting the password for each user and updated in the Task2 document.**

# Create and Secure Workspace Directories

Make individual workspace directories:
sudo mkdir -p /home/Sarah/workspace
sudo mkdir -p /home/mike/workspace

Set ownership so only Sarah and Mike can access their directories

sudo chown Sarah:Sarah /home/Sarah/workspace
sudo chmod 700 /home/Sarah/workspace

sudo chown mike:mike /home/mike/workspace
sudo chmod 700 /home/mike/workspace

# Verify permissions:

ls -ld /home/Sarah/workspace /home/mike/workspace

# Enforce Password Expiry (30 Days)

Set password expiry:

sudo chage -M 30 Sarah
sudo chage -M 30 mike

Check the settings:

sudo chage -l Sarah
sudo chage -l mike

**Note: Screenshots for the change output showing "Maximum days between password change: 30" for each user in Task2 document**

# Enforce Password Complexity

Edit the password policy (for strong passwords):

minlen = 8
dcredit = -1
ucredit = -1
ocredit = -1
lcredit = -1
