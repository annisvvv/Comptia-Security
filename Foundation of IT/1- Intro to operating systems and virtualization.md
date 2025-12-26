A computer system consists of a hardware and software linked by the operating system.
### Computer components
- CPU central processing unit
- RAM random access memory
- Storage HDD or SSD
- Motherboard
- PSU power supply unit
- I/O devices
### Operating system
the OS controls :
- Resource management : control CPU time, memory allocation, storage use
- Process management : manages active programs and background services
- Memory management : isolate processes in memory to prevent conflicts
- File system management : organize files and directories
- Device management : drivers to communicate with hardware
- User interface : CLI, GUI
### Virtualization
#### Hypervisor
- **Type 1:** Runs directly on hardware (e.g., Hyper-V, ESXi)
- **Type 2:** Runs on top of a host OS (e.g., VirtualBox, VMware Workstation)
### Some Linux commands

file system navigation :
- ls -l: Displays detailed file information (permissions, ownership, size).
- ls -a: Includes hidden files in the listing.
- cd [path]: Changes the current directory
- pwd: Displays the full path of the current working directory.

file and folder management :
- mkdir foldername: Creates a new directory named _foldername_.
- touch filename: Creates an empty file named _filename_.
- rm filename: Deletes a file.
- rm -r foldername: Deletes a directory and all its contents recursively.
- cp source destination: Copies files or folders.
    - cp -r source_folder target_folder: Recursively copies a directory.
- mv source destination: Moves a file or folder to a new location.
    - mv oldname newname: Renames a file or folder.

viewing system information :
- uname: Displays system information.
    - uname -a: Shows complete system details (kernel, architecture, etc.).
- whoami: Prints the username of the current user.
- df: Reports disk space usage.
	- df -h: Displays disk usage in a human-readable format (GB, MB).
- free: Shows memory usage.
    - free -m: Displays memory statistics in megabytes.
