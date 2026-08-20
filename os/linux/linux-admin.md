# Linux admin guide

- [Linux admin guide](#linux-admin-guide)
  - [System information](#system-information)
  - [System security](#system-security)
    - [Users](#users)
    - [Groups](#groups)
  - [Processes](#processes)
  - [Hardware](#hardware)
    - [Hardware status](#hardware-status)
    - [Hardware information](#hardware-information)
    - [sysstat](#sysstat)
  - [Network](#network)
  - [System managed services (systemd)](#system-managed-services-systemd)
  - [Docker](#docker)
  - [Kubernetes](#kubernetes)
  - [Filesystem](#filesystem)
    - [File operations](#file-operations)
    - [Permissions \& ownership](#permissions--ownership)
    - [Storage \& disk management](#storage--disk-management)
    - [Archiving \& transfer](#archiving--transfer)
  - [Logs \& journals](#logs--journals)
  - [Manuals](#manuals)
  - [Utilites](#utilites)
  - [System enviornment variables](#system-enviornment-variables)

## System information

| Command | Description |
| --- | --- |
| `uname` | Print kernel name, version and architecture |
| `hostname` | Show or set the hostname |
| `uptime` | Show how long the system has been running and load average |
| `date` | Show or set the system date and time |
| `timedatectl` | Show and manage time, date and timezone |
| `arch` | Print the machine architecture |
| `lsb_release` / `cat /etc/os-release` | Show distribution name and version |

## System security

| Command | Description |
| --- | --- |
| `sudo` | Execute a command with superuser privileges |
| `su` | Switch user (defaults to root) |
| `sudo -l` | List the privileges the user can run with sudo |
| `visudo` | Safely edit the sudoers file |
| `last` | Show a list of last logged in users |
| `who` | Show who is logged on the system |
| `w` | Show who is logged on and what they are doing |
| `ssh` | Secure shell: connect to a remote system |
| `ufw` | Manage the firewall (uncomplicated firewall) |

### Users

| Command | Description |
| --- | --- |
| `adduser` / `useradd` | Add a user |
| `usermod` | Modify a user account |
| `deluser` / `userdel` | Delete a user |
| `passwd` | Change the user's password |
| `chage` | Change user password expiry information |
| `id` | Show the UID and GID of a user |
| `whoami` | Show the current logged-in user |

### Groups

| Command | Description |
| --- | --- |
| `addgroup` / `groupadd` | Add a group |
| `delgroup` / `groupdel` | Delete a group |
| `groupmod` | Modify a group (name, GID) |
| `gpasswd` | Manage group membership and group password |
| `groups` | Show the groups of the current user |
| `getent group` | Query the group database |

## Processes

| Command | Description |
| --- | --- |
| `ps` | List running processes (snapshot) |
| `top` / `htop` | Show processes in real time (`htop` if installed) |
| `pgrep` | Find processes by name |
| `kill` | Send a signal to a process (default TERM) |
| `pkill` | Kill processes by name |
| `killall` | Kill all processes with a given name |
| `nice` | Run a process with a specific priority |
| `renice` | Change the priority of a running process |
| `nohup` | Run a process that keeps running after logout |
| `bg` / `fg` | Send a job to background / bring it to foreground |
| `jobs` | List background jobs of the current shell |
| `ulimit` | Show or set resource limits of the shell (open files `-n`, processes `-u`) |
| `lsof` | List open files / file descriptors, per process (`-p <pid>`) |
| `fuser` | Identify processes using a file or directory |
| `prlimit` | Get or set resource limits of a running process |

## Hardware

### Hardware status

| Command | Description |
| --- | --- |
| `free` | Show memory usage (RAM and swap) |
| `sensors` | Show temperatures, voltages and fan speeds (lm-sensors) |
| `smartctl` | Check disk health (SMART data) |
| `hddtemp` | Show disk temperature |

### Hardware information

| Command | Description |
| --- | --- |
| `lscpu` | Show CPU information |
| `lspci` | List PCI devices |
| `lsusb` | List USB devices |
| `lsblk` | List block devices (disks and partitions) |
| `dmidecode` | Dump hardware information (BIOS, memory, etc.) |
| `lshw` | List hardware details |

### sysstat

| Command | Description |
| --- | --- |
| `mpstat` | Show CPU usage per processor (and per core) |
| `iostat` | Show CPU and disk I/O statistics |
| `pidstat` | Show per-process performance statistics |
| `sar` | Collect, report or replay system activity data |
| `sadf` | Export sar data in other formats (CSV, XML, ...) |

## Network

| Command | Description |
| --- | --- |
| `ip` | Show/manage interfaces, addresses and routes |
| `ifconfig` | Show or configure network interfaces |
| `ping` | Test connectivity to a host |
| `traceroute` | Show the route packets take to a host |
| `ss` | Show socket statistics (open ports and connections) |
| `netstat` | Show network connections, routing tables and interfaces |
| `dig` / `nslookup` | Query DNS records |
| `curl` | Transfer data from/to a URL |
| `wget` | Download files from a URL |
| `ethtool` | Show/configure network device settings |
| `nmap` | Network scanner (hosts and open ports) |

## System managed services (systemd)

| Command | Description |
| --- | --- |
| `systemctl` | Manage systemd services and the system |
| `systemctl start/stop/restart <svc>` | Start, stop or restart a service |
| `systemctl enable/disable <svc>` | Enable or disable a service at boot |
| `systemctl status <svc>` | Show the status of a service |
| `systemctl list-units` | List loaded units (services, sockets, ...) |
| `systemctl list-timers` | List scheduled timers |
| `systemctl --failed` | List failed units |
| `systemctl mask/unmask <svc>` | Fully block or unblock a unit |
| `systemd-analyze` | Analyze system boot performance |
| `shutdown` | Shut down or restart the system |
| `reboot` | Reboot the system |
| `poweroff` | Power off the system |

## Docker

| Command | Description |
| --- | --- |
| `docker run` | Run a container from an image |
| `docker ps` | List running containers (`-a` for all) |
| `docker stop` / `docker start` | Stop or start a container |
| `docker rm` | Remove a container |
| `docker images` | List local images |
| `docker pull` | Download an image from a registry |
| `docker build` | Build an image from a Dockerfile |
| `docker exec -it <ctr> sh` | Open a shell inside a running container |
| `docker logs <ctr>` | Show the logs of a container |
| `docker compose up/down` | Start or stop a Compose stack |
| `docker network ls` | List Docker networks |
| `docker volume ls` | List Docker volumes |

## Kubernetes

| Command | Description |
| --- | --- |
| `kubectl get <res>` | List resources (pods, nodes, services, ...) |
| `kubectl describe <res>` | Show detailed information of a resource |
| `kubectl apply -f <file>` | Create or update resources from a YAML manifest |
| `kubectl delete <res>` | Delete a resource |
| `kubectl logs <pod>` | Show the logs of a pod |
| `kubectl exec -it <pod> -- sh` | Open a shell inside a pod |
| `kubectl port-forward <pod>` | Forward a local port to a pod |
| `kubectl scale deploy <name> --replicas=N` | Scale a deployment |
| `kubectl rollout status` | Track the status of a rollout |
| `kubectl top node` / `kubectl top pod` | Show node / pod resource usage |
| `kubectl config get-contexts` | List kubeconfig contexts |
| `kubectl drain <node>` | Safely evict pods from a node |

## Filesystem

### File operations

| Command | Description |
| --- | --- |
| `ls` | List files and directories |
| `pwd` | Show the current directory |
| `cd` | Change directory |
| `mkdir` | Create directories |
| `rmdir` | Remove empty directories |
| `touch` | Create an empty file or update timestamps |
| `cp` | Copy files or directories |
| `mv` | Move or rename files |
| `rm` | Delete files or directories |
| `ln` | Create links (hard, or symbolic with `-s`) |
| `find` | Search files by name, type, size, etc. |
| `tree` | Show the directory tree |
| `stat` | Show detailed file information |
| `file` | Show the file type |

### Permissions & ownership

| Command | Description |
| --- | --- |
| `chmod` | Change file permissions |
| `chown` | Change file owner and group |
| `chgrp` | Change file group |

### Storage & disk management

| Command | Description |
| --- | --- |
| `df` | Show disk space usage of filesystems |
| `du` | Show disk usage of files and directories |
| `mount` / `umount` | Mount or unmount filesystems |
| `fdisk` | Partition a disk |
| `mkfs` | Create a filesystem on a partition |
| `fsck` | Check and repair a filesystem |
| `blkid` | Show block device attributes (UUID, label) |
| `dd` | Low-level copy (e.g. disk images) |
| `sync` | Flush filesystem buffers to disk |

### Archiving & transfer

| Command | Description |
| --- | --- |
| `tar` | Create or extract archives |
| `rsync` | Sync files locally or remotely |
| `scp` | Copy files over SSH |
| `gzip` / `gunzip` | Compress / decompress files |
| `zip` / `unzip` | Compress / extract zip archives |

## Logs & journals

| Command | Description |
| --- | --- |
| `journalctl` | Read the systemd journal logs |
| `journalctl -u <svc>` | Show logs of a specific service |
| `journalctl -f` | Follow logs in real time |
| `dmesg` | Kernel ring buffer (boot and hardware messages) |
| `tail` | Show the last lines of a file (`-f` to follow) |
| `head` | Show the first lines of a file |
| `less` | View files page by page, with search |
| `logrotate` | Rotate, compress and delete old log files |
| `logger` | Write a message to the system log |

## Manuals

| Command | Description |
| --- | --- |
| `man <cmd>` | Show the manual page of a command |
| `info <cmd>` | Show the info documentation of a command |
| `whatis <cmd>` | One-line description of a command |
| `apropos <keyword>` | Search manual pages by keyword |
| `<cmd> --help` / `<cmd> -h` | Quick help of a command |

## Utilites

| Command | Description |
| --- | --- |
| `grep` | Search text patterns in files or output |
| `sed` | Stream editor (search and replace in streams) |
| `awk` | Text processing and report generation |
| `sort` | Sort lines of text |
| `uniq` | Remove or report duplicate lines |
| `cut` | Extract columns or fields from lines |
| `tr` | Translate or delete characters |
| `wc` | Count lines, words and characters |
| `cat` | Concatenate and print files |
| `echo` | Print a message or a variable |
| `xargs` | Build and run commands from standard input |
| `watch` | Run a command repeatedly and show the output |
| `tee` | Write output to a file and to the screen |
| `which` | Show the path of a command |
| `history` | Show the command history |
| `alias` | Create a shortcut for a command |
| `tmux` / `screen` | Terminal multiplexer (multiple sessions) |

## System enviornment variables

| Command | Description |
| --- | --- |
| `echo $VAR` | Show the value of a variable |
| `env` | Show all environment variables |
| `printenv <VAR>` | Show the value of an environment variable |
| `export VAR=value` | Set and export an environment variable |
| `unset VAR` | Remove an environment variable |
| `set` | Show shell and environment variables |
| `source <file>` | Load variables from a file (e.g. `~/.bashrc`) |
| `/etc/environment` | Global environment variables file |
| `/etc/profile`, `~/.bashrc`, `~/.zshrc` | Shell config files where variables are defined |
