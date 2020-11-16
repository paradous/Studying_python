# List of commands

This file contains a list of useful commands on Linux. The descriptions down
below are far from complete, they are only here to give an idea of the use case.
Plus, there are many more commands and terminal tools out there for all sorts of
needs, feel free to research. 

NOTE: Not all commands are necessarily installed on your system.

## Help

* `man`: display system documentation.
``` Shell
man man
man touch
```
* `whatis`: prints manual page description.
``` Shell
whatis man
whatis shell
```
* `info`: read _Info_ documents.
``` Shell
info ls
info cp
```
* `--help`: show the help for the desired package. **useful !**
``` Shell
ls --help
chmod --help
```

## Navigation

* `cd`: change current directory. **useful !**
``` Shell
cd /home/becode/Desktop/
cd # Go to home directory
cd / # Go to root directory
cd .. # Go to parent directory
```
* `ls`: list directory content. **useful !**
``` Shell
ls
ls -l file.txt # Show the permissions and other details of the file
```
* `pwd`: print the current directory.
* `pushd`: go to a folder while keeping old location on _"cache"_.
* `popd`: go back to an old location on _"cache"_.


## File operation

* `cat`: concatenate and print files. **useful !**
``` Shell
cat > file.txt # Create file.txt and append text. Leave editor with CTRL+C
```
* `touch`: create a file or update timestamps. **useful !**
``` Shell
touch file.txt # Create file.txt
echo "Hello World" > file.txt # Append one line to the file
```
* `cp`: copy a file or a folder with files, to a location **useful !**
``` Shell
cp file.txt file_new.txt # Copy a file in the same folder
cp file.txt sub/directory # Copy file.txt to ./sub/directory and store it as file.txt
cp -r sub sub_new # Copy the directory sub and its content to sub_new
```
* `mkdir`: create a directory. **useful !**
* `mv`: move or rename a file. **useful !**
``` Shell
mv file.txt file2.txt # Rename file.txt to file2.txt
mv file.txt sub/directory # Move file.txt to sub/directory
```
* `rm`: remove a file or directory. **useful !**
``` Shell
rm -rf folder # Remove a directory and all of its content
rm file.txt # Remove a file
```
* `rmdir`: remove an empty directory.
* `ln`: link files.
* `head`: output the first part of files.
* `tail`: output the last part of files.


## System

* `date`: print the date and time
* `cal`: display a calendar
* `lsblk`: list connected drives


## Users

* `passwd`: change user password
* `usermod`: modify a user account
* `groupadd`: create a new group
* `whoami`: print current logged user


## Permissions

**Pro tip:**
```
ls -l file.txt # Show the permissions and other details of the file
```

* `sudo`: execute a command as another user
* `su`: change the current user
* `chmod`: change file permissions
```
chmod u=rwx,go=rwx,o-rwx file.txt # Set permissions to rwx for owner and group. Remove all permissions for other.
# r = read, w = write, x = execute
# u = owner, go = group, o = other, a = all
```
* `chown`: change the owner of a file
* `chgrp`: change the group of a file


## Compression

* `tar`: archive files
* `gzip`: compress and expand files


## Remote

* `ssh`: remote login
* `rsync`: remote file copying tool


## Process management

* `ps`: report process status
* `kill`: stop a process
* `top`: display list of running processes
* `htop`: improved version of `top`
* `bg`: put a process on the background
* `fg`: bring a process on the foreground


## Package manager

* `apt-get`
* `pacman`
* `pip`
* `npm`
* `composer`


## Text editor

* `vim`
* `nvim`
* `nano`
