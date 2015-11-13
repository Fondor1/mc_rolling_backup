# mc_rolling_backup
A rolling minecraft server backup solution for Linux

In order to mitigate minecraft server data loss, this tool aims to provide a solution for periodic rolling backups.

## Requirements

* A working Minecraft server
* [Minecraft Server Manager](https://github.com/msmhq/msm) (MSM)
* Python 3
* cron

## Description
A rolling backup system was chosen to accomodate the need for frequent backups but also resist the buildup of old backup files to save disk space. The chosen backup solution is separated into three rolling cycles and one continuous cycle:

* An hourly backup is created for the last 24 hours
* A daily backup is created for the past seven days
* a weekly backup is created for the past five weeks
* a monthly backup is created every month

The first three backups roll over after the stated duration has passed. As an example: when a server is started, new backup files are recorded every hour for 24 hours. On the 25th hour since startup, the oldest hourly backup is removed and replaced with a new backup file. The other 23 hour backup files are left untouched. This rolling cycle continues indefinitely. This contrasts with the monthly continuous backup cycle, which records a new backup once at the start of every month and does not remove any previous backups.

The total number of backup files created will start at 24 + 7 + 4 + 1 = 36 and will steadily increase by 1 backup file each month that the server remains online.
