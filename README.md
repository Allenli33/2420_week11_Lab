ACIT 2420 Linux Week 11 Lab
===============

Completed by Hened Medina and Hao Li


This README.MD guides how to do the following:
----------------------------------------------
1. Backup Directories from one server to a backup-server at 1am on Friday.
2. Viewing Weather Forecast from a specific specity at 5am everyday.

**Note:** Each instructions has its own script, service file, and timer file found in the repo



Resources/Technologies Used
-------------------------------

- WSL - Windows Subsystem for Linux (Ubuntu)
- DigitalOcean Droplets
- Windows Terminal (with Administrative Privileges)


Prerequisites and Assumptions (DigitalOcean and WSL setup)
----------------------------------
**Note:** The following video is assumed to be watched. The video includes specific commands when setting up DigitalOcean Droplets. The setup instructions below are to be done once the user has watched the video.

Follow along the embedded video to setup [DigitalOcean Droplets](https://vimeo.com/758870226/f75da348fc?embedded=true&source=video_title&owner=17609105)

**Note:** 
Ensure to name the two droplets: **server-one** and **backup-server**. These will be the hostnames for your servers. These servers must have root privileges

WSL Setup
-------------------------

1. Install WSL on the  host machine with the following command: `wsl --install -d Ubuntu`
2. As root in **WSL**,  create a regular user with the following command: `useradd -ms /bin/bash`
3. Login as the newly created regular user


## 1. Installation

Clone the Repository in your Linux Machine using:

```
git clone https://github.com/username/2420_week11_Lab.git
```


## Creating the backup-script
1. Create a new file called backup-script in the home/week_11 directory. Use:
```
cd week_11/
sudo vim backup-script
```
2. Follow the content in the screenshot below for the backup-script file
![](images/backup-script.png)


## Creating the Configuration file
1. Create a new file called backup.conf in the /etc directory. Use:
```
sudo vim /etc/backup.conf
```
2. Follow the content in the screenshot below for the configuration file

![](images/backupconf.png)

3. Save and exit your backup.conf file

4. Copy the backup-script and the backup-timer files in the `/etc/systemd/system` directory using the commands shown in the screenshot below

![](images/image12.png)

5. Within the /opt directory, created a new directory called bakcup

6. After you created backup folder copy your backup script in your backup to make sure is matching your service file so it can be run 
![](images/cpbackup.png)
![](images/image20.png)


## Creating the Service File
1. Use the Command to create a new service file:
```
sudo vim backup.service
```
2. Follow the content in the screenshot below for the service file

![](images/image14.png)

**Note:** The Description describes what the script will do

3. Save and exit the backup.service in vim

## Creating the Timer File
1. Use the Command to create a new timer file:
```
sudo vim backup.timer
```
2. Follow the content in the screenshot below for the timer file

![](images/image7.png)

3. Save and exit the backup.timer in vim

## Starting the Service and Checking its Status
1. To reload the daemon, use the command: `sudo systemctl daemon-reload`
2. To start the service file, use the command: `sudo systemctl start backup.service`
3. To check the status of the service file, use the command: `sudo systemctl status backup.service`
** Check to see if the output matches the screenshot below**

![](images/image19.png)

4. To check to see if the timer is working, use the command: `sudo systemctl list-timers`
** Check to see if the output matches the screenshot below**

![](images/image17.png)

