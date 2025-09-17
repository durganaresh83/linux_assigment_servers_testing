# Backup Configuration for Web Servers
  Objective: Configure automated backups for Sarah’s Apache server and Mike’s Nginx server to ensure data integrity and recovery.

# Prepare the Backup Directory

sudo mkdir -p /backups
sudo chmod 700 /backups

This creates a secure backup folder. 
Screenshot the output of ls -ld /backups to show directory permissions and updated the Task3 document

# Create the Backup Scripts

(A) Sarah’s Apache Backup Script
  Create the script:
  sudo nano /usr/local/bin/apache_backup.sh
