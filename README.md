Section 1: rsyslog Rules

1- What are the key components of an Rsyslog rule?
* The key components of an rsyslog are ( Facility, Priority ).

2- How do facility and severity levels work in rsyslog?
* In rsyslog, facilities and severity levels work together to categorize and prioritize log messages.

3- Describe how you would configure rsyslog to write auth logs to a separate file.
* sudo nano /etc/rsyslog.d/auth.conf
* auth,authpriv.*    /var/log/auth.log
* sudo touch /var/log/auth.log
* sudo chmod 600 /var/log/auth.log
* sudo systemctl restart rsyslog

4- How can you test whether the custom rsyslog rule that you just created is working?
* ssh invaliduser@localhost
* sudo tail /var/log/auth.log
* sudo systemctl stop rsyslog
* sudo rsyslogd -dn
* sudo systemctl start rsyslog

________________________________________________________________________________________________________________________
Section 2: Log File Rotation

1-What is the purpose of log file rotation?
* Limiting Log File Size
* Archiving Old Logs
* Maintaining System Performance
* Ensuring Data Retention
* Automating Cleanup

2- How does logrotate determine when to rotate a log file?
* logrotate decides when to rotate a log based on the rules defined in its configuration files, usually located, /etc/logrotate.conf, /etc/logrotate.d/

3- Describe a typical logrotate configuration for daily rotation and keeping 7 backups.
* /var/log/yourlogfile.log 
    daily            
    rotate 7         
    compress          
    missingok         
    notifempty       
    create 0640 root adm 

  4- How can you manually trigger a log rotation for testing purposes?


___________________________________________________________________________________________________________________________
Section 3: systemd-journald

1- What is the difference between journald and rsyslog?
* journald:
Local system diagnostics
Structured and rich metadata logs
Viewing logs with journalctl
* rsyslog:
Forwarding logs to central log servers
Parsing, filtering, and storing logs in custom formats
Interfacing with log analysis tools (e.g., ELK stack)

2- Where does journald store log data by default?
* /run/log/journal/

3- How can you configure journald to persist logs across reboots?
* sudo mkdir -p /var/log/journal
* sudo nano /etc/systemd/journald.conf
* Storage=persistent
* sudo systemctl restart systemd-journald
* journalctl --disk-usage
* sudo reboot journalctl

4- How do you view logs for a specific service using journalctl?
* journalctl -u <service_name>.service

_______________________________________________________________________________________________________________________________
Section 4: Network Troubleshooting Tools

1- What kind of information can you gather using traceroute?
* traceroute is a network diagnostic tool that shows the path that packets take from your machine to a destination.

2- What is the difference between netstat and ss?
* netstat	( old, slower, deprecated )
* ss	( Faster, modern, preferred tool )

3- How would you use dig to check if DNS is working correctly?
* dig is a command-line tool to query DNS servers and verify DNS resolution, dig google.com.

4- In what situations would you use tcpdump? What precautions should be taken?
* tcpdump is a powerful command-line tool used to capture and analyze network traffic directly on a system's network interfaces.
 
4-1 What precautions should be taken?
* Run as root (with caution)	( Full packet capture requires root privileges, but always use the least privilege possible )
* Avoid Capturing Sensitive Data Unnecessarily	( Packets may contain sensitive info (e.g., passwords if unencrypted); limit filters to specific traffic ).
* Encrypt/Protect Capture Files	 ( .pcap files can contain sensitive data and should be stored securely ).

5- How does nmap help in network discovery and security auditing?
* Discover devices on a network
* Identify open ports and running services
* Audit for vulnerabilities and misconfigurations

________________________________________________________________________________________________________________________________
Section 5: Cron Job for Backup

1- How do you schedule a cron job to run daily at midnight?
* 0 0 * * * /path/to/command

2- Write a cron job that creates a compressed backup of your user's home directory to /backup folder.
* 0 0 * * * tar -czf /backup/home_backup_$(date).tar.gz /home/user

3- Where can you view a list of current cron jobs for your user?
* crontab -l

4- How do you redirect cron job output to a log file?
* 0 0 * * * /home/user/backup.sh >> /var/log/backup.log

____________________________________________________________________________________________________________________________
Section 6: Package Management

1- What are the key differences between apt and yum package managers?
*                      apt                                                                                  yum 
     Debian-based systems: Ubuntu, Debian, Linux Mint	                                        RPM-based systems: RHEL, CentOS, Fedora
                  .deb packages                                                                          .rpm packages
         Uses APT repositories (sources.list)                                                   Uses YUM repositories (.repo files)
    	Simpler and more modern with apt (e.g., apt install)                                      Uses yum commands (e.g., yum install)

2- How do you add a new software repository in Debian-based systems?
* sudo nano /etc/apt/sources.list
* deb http://ppa.launchpad.net/nginx/stable/ubuntu
* sudo apt update

3- What command would you use to upgrade all installed packages on an Ubuntu system?
* sudo apt upgrade

4- Describe the steps to remove a package and its configuration files using apt.
* apt list --installed | grep nginx
* sudo apt purge nginx
* sudo apt autoremove

_______________________________________________________________________________________________________________________________












 

