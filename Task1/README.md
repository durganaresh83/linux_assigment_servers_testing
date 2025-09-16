# Task-1: System monitoring and Setup
Objective: Configure a monitoring system to ensure the development environment’s health, performance, and capacity planning.

# Install and configure monitoring tools

# Step 1: Install htop or nmon

sudo yum install epel-release -y
sudo yum install htop -y

# Verify install
htop

Output - Updated the screenshots in Task1 folder

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

# Step 3: Process and Resource Monitoring
process monitoring to identify resource-intensive applications.

# ps/grep for top CPU/memory users:

sudo bash -c "ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head > /var/log/sysmonitor/top_mem_processes_$(date +%F_%T).log"

# OUTPUT
    PID    PPID CMD                         %MEM %CPU
   2144       1 /usr/bin/amazon-ssm-agent    1.9  0.0
      1       0 /usr/lib/systemd/systemd --  1.7  0.0
   1096       1 /usr/lib/systemd/systemd-jo  1.5  0.0
   1769       1 /usr/lib/systemd/systemd-re  1.5  0.0
   2406       1 /usr/lib/systemd/systemd --  1.3  0.0
   1766       1 /usr/lib/systemd/systemd-ud  1.1  0.0
   2398    2148 sshd: ec2-user [priv]        1.0  0.0
   1966       1 /usr/lib/systemd/systemd-lo  1.0  0.0
   1971       1 /usr/lib/systemd/systemd-ne  1.0  0.0

 sudo bash -c "ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head > /var/log/sysmonitor/top_cpu_processes_$(date +%F_%T).log"

 # OUTPUT
     PID    PPID CMD                         %MEM %CPU
      1       0 /usr/lib/systemd/systemd --  1.7  0.0
      2       0 [kthreadd]                   0.0  0.0
      3       2 [rcu_gp]                     0.0  0.0
      4       2 [rcu_par_gp]                 0.0  0.0
      5       2 [slub_flushwq]               0.0  0.0
      6       2 [netns]                      0.0  0.0
      8       2 [kworker/0:0H-events_highpr  0.0  0.0
     10       2 [mm_percpu_wq]               0.0  0.0
     11       2 [rcu_tasks_kthread]          0.0  0.0

 # htop view (sort by CPU/Memory in htop):
  Launch htop, press F6, sort by "%MEM" and "%CPU", screenshot (**htop_sort_cpu_mem**) uploaded in Task1 folder.

# Step 4: Automate log collection with cron

Add cron jobs (example, runs every hour):

. Create a script as sysmonitor_logs.sh

    #!/bin/bash
    TIMESTAMP=$(date +'%F_%T')
    
    htop -b -n 1 > /var/log/sysmonitor/htop_hourly_${TIMESTAMP}.log
    df -h > /var/log/sysmonitor/df_hourly_${TIMESTAMP}.log
    ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head > /var/log/sysmonitor/topcpu_hourly_${TIMESTAMP}.log
    
    chmod +x sysmonitor_logs.sh
    
    edit crontab -e and add the below command
    0 * * * * /usr/local/bin/sysmonitor_logs.sh - it will run every hour
    */15 * * * * /usr/local/bin/sysmonitor_logs.sh - it will run every 15mins

# OUTPUT files are added to Task1 folder
Below are the file names

    . top_cpu_processes_2025-09-16_15-01-26.log
    . df_hourly_2025-09-16_15\-34\-19.log
    . **htop hourly report generated empty file and tried for 10mins as well but not generated empty file**






