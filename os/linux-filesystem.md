# Filesystems

Linux traditional filesystem is ext4 type. Despite XFS and BTRFS are also well know types.

Filesystems are an OS abstraction to manage file storage.

## Classic structure at /

* / (Root): The top-level directory containing all other files, folders, and attached devices
* ./bin: Essential command binaries (like ls and cat) needed for basic system repair and user operations
* ./boot: Static boot loader files, kernel images, and RAM disk files required during startup
* ./dev: Device nodes and hardware files, reflecting the Unix rule that everything is a file./etc: System-wide configuration files and startup scripts
* ./home: Personal directories for regular users, holding individual settings and data./lib: Essential shared libraries and kernel modules required to boot and run executables./media: Mount points for removable media like USB flash drives or CDs
* ./mnt: Temporary mount points traditionally used by administrators for manual file systems
* ./opt: Optional or third-party software application packages
* ./proc: Virtual filesystem exposing runtime information about processes and kernel parameters
* ./root: Home directory specifically for the root (administrative) user
* ./sbin: System administration binaries meant for root execution (like fdisk or reboot)
* ./sys: Modern virtual interface detailing device and driver configurations managed by the kernel
* ./tmp: Transient space for temporary files that are usually wiped on reboot
* ./usr: Secondary hierarchy housing read-only user utilities, shared libraries, and documentation./var: Variable data that changes over time, including system logs (/var/log), mail spools, and databases.

## Mounting points



## Network Filesystem (NFS)

At `/etc/exports` file each machine defines which folders are exportable.

Using `exportfs -v server_addr` the client could check which folders are available at that server.
