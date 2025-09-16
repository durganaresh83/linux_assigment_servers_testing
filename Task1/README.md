# Task-1: System monitoring and Setup
Objective: Configure a monitoring system to ensure the development environment’s health, performance, and capacity planning.

# Install and configure monitoring tools

# Step 1: Install htop or nmon

sudo yum install epel-release -y
sudo yum install htop -y

# Verify install
htop

Output - Updated the screenshots in Task 1 document

# Disk Usage Monitoring

# Step 2: Track storage with df and du

df (shows overall disk usage):

df -h 
# OUTPUT
**Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        4.0M     0  4.0M   0% /dev
tmpfs           475M     0  475M   0% /dev/shm
tmpfs           190M  444K  190M   1% /run
/dev/xvda1      8.0G  1.6G  6.4G  20% /
tmpfs           475M     0  475M   0% /tmp
/dev/xvda128     10M  1.3M  8.7M  13% /boot/efi
tmpfs            95M     0   95M   0% /run/user/1000**

df -h > /var/log/sysmonitor/df_output_$(date +%F_%T).log

du (shows folder/file sizes)

du -sh /home/*

**Output: 20K	 /home/ec2-user**

