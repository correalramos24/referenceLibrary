# Ubuntu 

Basic concepts to manage an Ubuntu server machine

- [Ubuntu](#ubuntu)
  - [Hostname](#hostname)
  - [User (and super-user) management](#user-and-super-user-management)
  - [Folder and files permissions management](#folder-and-files-permissions-management)
  - [Environment variables](#environment-variables)
  - [Jobs and processes](#jobs-and-processes)
  - [Netplans](#netplans)
  - [System logs](#system-logs)



## Hostname

Located at `/etc/hostname`. Need to reboot the machine to see the changes.
The environment variable `$HOSTNAME` stores the hostname value.

## User (and super-user) management

* adduser / useradd: To add a user.
* addgroup / groupadd: To add a group.
* usermod: To modify a user account.
* deluser / userdel: To delete a user.
* delgroup / groupdel: To delete a group.
* passwd: To change the user’s password.

* To list the groups of one user `groups username`. For all the groups use `compgen -g`.
* To list all the user, use `compgen -u`.

The variable `$USER` points to the user name.

* Make user superuser:  sudo usermod -aG sudo james (Run this commando from a super-user account).

To run a command with super-user powers, you need to use either the `sudo` command or open a terminal with super-user with `sudo su`.

## Folder and files permissions management

* Permission bits: **r**ead, **w**rite, **e**xecute (stands also for 4,2 and 1 values).
  * r (allows ls), w (allow create-delete files), e(cd into directory)
* User restriction levels: owner, group, other.
* The superusers have all the permissions enabled.

The permisions can be changed with the change file mode bits (`chmod`); also the owner can be changed with change owner (`chown`).

## Environment variables


## Jobs and processes
You can run a program in background with `&` at the end of the command line order, to see all the background processes you can use the command `jobs`.
Also is possible to suspend a program with `Ctlr+Z` and return to the execution in:
* Background with `bg`
* Foregrond with `fg`
Followed by job id you want to resume (1 by default).

To cancell a job, use `Ctrl+C` for the foreground process or use kill either with the pid or the job id.

## Netplans

## System logs





