# Forensic-Imaging
This repository contains the necessary actions taken during the Forensic Imaging process and the commands and tools used

## Preparation
- The process of imaging a disk starts by identifying the target drive, preparing it for imaging, and then creating the image file which is later verified for integrity. This needs to be performed in an 
  environment that allows us to perform these tasks and also ensures the process is properly logged.
- Each operating system has specific file system structures and configurations that require different imaging tools and techniques. In our scenario, we will use Linux as the OS to acquire the data and 
  create a forensic image of a drive. The use of open-source software for image acquisition is an advantage in many cases since it can satisfy guidelines for evidential reliability that need to be 
  fulfilled. The Linux kernel also supports many file systems, which is a big advantage when analyzing different media types.
  ### Write-Blockers
  - It is important to mention that write-blockers are usually required when manipulating physical disks. A write-blocker is a device used to prevent any modifications to data on a storage 
    device during analysis. It ensures reading data without risking changes to the original evidence. Write-blockers work by physically intercepting all drive commands that write data sent between the 
    disk being imaged and the OS attached to it.
  ### Audit Trail
  - An audit trail is a chronological record that tracks actions and events within a system, providing a detailed history for accountability and security. It ensures traceability by documenting each step. 
    This step can be performed with different parameters depending on the legal or compliance framework required by the task.
  - We can manually or automatically record the actions and events with varying detail levels. Since we need to preserve the evidence and keep track of our activities, let's explore some methods for 
    tracking tasks and automating command-line activity logging to help us have this audit trail of our process.
  - If we are using bash, the history command can help us log our activity. It can be saved using a timestamp and preserved in a file. Below, we can observe a chart with some commands recommended to use 
    during our session.
    - ```set -O history```                 : Enables command history in the shell, allowing it to record the commands you enter.
    - ```shopt -s histappned```            : Ensures that the command history is appended to the history file instead of overwriting it when the shell exits.
    - ```export HISTCONTROL=```            : Clears any settings that control which commands are saved in the history, ensuring all commands are recorded.
    - ```export HISTIGNORE=```             : Clears any settings that ignore specific patterns of commands, so all commands are saved in the history.
    - ```export HISTFILE=~/.bash_history```: Sets the file where the command history is saved.
    - ```export HISTFILESIZE=-1```         : Sets no limit on the number of lines stored in the history file.
    - ```export HISTSIZE=-1```             : Sets no limit on the number of commands retained in the shell history.
    - ```export HISTTIMEFORMAT="%F-%R "``` : Formats timestamps in the history as "YYYY-MM-DD HH" for each command.

  ### Accessing the File System
  - ```df```                    : Used to see the attached devices on the target machine.
  - ```lsblk```                 : List block devices
  - ```lsblk -a ```             : List all devices
  - ```losetup -l```            : Used to get the more info about the device
  - ```blkid <Interface Name>```: Used to acquire further information like the UUID of the image
 
## Creating a Forensic Image
- ```.img``` extension is used to identify the file as an image.
  ### Tools
  - ```dd```                    : A standard Unix utility for copying and converting files, often used for creating raw disk images
  - ```dc3dd```                 : An enhanced version of ```dd``` with additional features for forensic imaging, including hashing and logging
  - ```ddrescue```              : A data recovery tool that efficiently copies data from damaged drives, attempting to rescue as much data as possible
  - ```FTK Imager```            : A GUI-based tool for creating forensic images, widely used for its ease of use and comprehensive features
  - ```GuyMager```              : A GUI-based forensic imaging tool that supports various image formats and provides detailed logs
  - ```EWF Tools (ewfacquire)```:  Tools for creating and handling Expert Witness Format (EWF) images, often used in digital forensics
  ### Integrity Checking
  - ```md5sum```

### Other types of Imaging
- Remote Imaging: Involves creating an image over the network, allowing it to acquire data without physical access to the device.
- USB Images    : Creates an image of a USB drive's contents.
- Docker Images : While not strictly an image, it creates a snapshot of a Docker container's filesystem and configuration.

### Mount Commands
- Create a mount directory
  ```
  sudo mkdir -p /mnt/<directory name>
  ```
- Mount the Image
  ```
  sudo mount -o loop <image name>.img /mnt/<directory name>
  ```
