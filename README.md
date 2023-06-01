# Backup-of-Linux-server
Step by step guide to backup Linux machine

The Linux command line provides several utilities for creating and restoring backups. The tar command can be used to create compressed archives of files and directories. The dd command can be used to copy and restore drives and partitions, and to create image files of drives and partitions that can be used for backups. 

Both archives and image files, as well as regular files and directories, can be remotely synced using the rsync command. In this lab, you will be tasked with using these utilities to back up important data on a Linux host and sync it to a backup server.

Objectives

Successfully complete this lab by achieving the following learning objectives:

Use the tar Command to Create Backups of Directories on the server01 Host

Create an archive called full_bkp.tgz in /home/cloud_user using gzip compression on the following directories: /home, /etc, /opt, /usr/local, /root, and /srv.

Create an archive called var_bkp.tbz in /home/cloud_user of the /var directory using bzip2 compression.


Use the dd Command to Create and Restore Backups of Devices on the server01 Host


Use /home/cloud_user/xvdg.img to restore the /dev/xvdg device (use a byte size of 4MB).

Create an image file of /dev/xvdf in /home/cloud_user/, and call it xvdf.img.bz (it should be compressed with bzip2).

Once the xvdf.img.bz file has been created, wipe the /dev/xvdf device using the /dev/zero device.


Synchronize Backups to server02 Using the rysnc Command on the server01 Host

Sync (with compression) var_bkp.tbz and full_bkp.tgz to /home/cloud_user/archive on server02. Permissions and timestamps should be preserved.

Sync xvdf.img.bz to /home/cloud_user/archive. Do not use archive mode or compression.

Sync (with compression) the following directories to /home/cloud_usr/sync on server02: /home, /etc, /opt, /usr/local, /var/lib, /var/log, /root, /srv. Permissions and timestamps should be preserved.


Validate the Backup Files and Directories Were Successfully Copied on the server02 Host

List the contents of the /home/cloud_user/archive directory.

List the contents of the /home/cloud_user/sync directory.


Tar -cvzf /home/chris/full_bkp.tgz  /home/ /etc/  /opt/ /usr/local/ /root/ /srv

Tar -cvjf  /home/user/var_bkp.tbz  /var/

Listing on home dir to see the backup

ll /home/user

lsblk // shows the mount point

Restore image file

Dd if=/home/user/xvdg.img of=/dev/xvdg bs=4M

It will shows the size copied and the time in secs

Run lsblk 

Dd if=/dev/xvdf bs=4M | bzip2 -c > /home/user/xvdf.img.bz

Run ll -h /home/user/

Wipe the device

Dd if=/dev/zero of=/dev/xvdf bs=4M

Run lsblk to validate

Sync to server 2

Rsync -avzh /home/user/var_bkp.tbz /home/user/full_bkp.tgz cloud@ip add of server2:/home/user/archive

Enter key and password

Will show file size sent.

Rysnc -vh /home/user/xvdf.img.bz loud@ip add of server2:/home/user/archive

Rysnc -avzh  /home /etc /opt /usr/local /var/lib /var/log /root /srv cloud_user@ipaddres:/home/user/sync

Validate; log in to server 2

Listing f home directory

ll -h /home/user/archive

ll -h /home/user/sync/
