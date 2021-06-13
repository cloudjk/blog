---
title: Linux Command Line Basic
sidebar: mydoc_sidebar
permalink: linux_command_line_basic.html
folder: linux
---
## ls
```bash
man ls      # show all options
ls -al      # list all folders, files including hidden files as a long format
ls -ltr     # list all folders and files in reverse time order as a long format
ls -R       # list subdirectories recursively
```
## cat
```bash
man cat            # show all options
cat -b list1.txt   # add line number in non-blank line
cat -n list1.txt   # add line number in all lines
cat -s list1.txt   # squeeze blank lines to one blank line
cat -E list1.txt   # add $ sign to the end of each line
cat -v list1.txt   # display non-printing characters.
```

## Redirection
```bash
# Redirection ( > or >> ) can be used in other commands as well like ls, cd ...
ls -al > result.txt

# Redirection one angle bracket : overwrite
cat > test.txt
line 1    # enter in command line
line 2
cat > test.txt
line 3
line 4
# => result (overwrite)
line 3
line 4

# Redirection double angle bracket : append
cat >> test.txt
line 1
line 2
cat >> test.txt
line 3
line 4
# => result (no overwrite)
line 1
line 2
line 3
line 4

# Redirection with files
cat list1.txt list2.txt > out.txt    # concatenate list1 and list2 then transfer output to out.txt file
cat list1.txt list2.txt > list2.txt  # invoke error and should be changed like below (input and output should be different)
cat list1.txt >> list2.txt 
```

## mkdir
```bash
# Create a parent directory and a sub directory at the same time
mkdir -p parent/child1/child2/child3

#Create a parent directory and mutiple sub directories at the same time
mkdir -p parent/{john,mark,ken}  :: without space between commas
```

## rm
```bash
man rm
# rm -rf :: f (without prompt)
# rm -rfv :: v (verbose shows extra info)
```

## cp
```bash
# copy file1.txt to file2.txt (if file2.txt does not exist then it creates file and copy)
cp file1.txt file2.txt 

# copy file to existing directory
cp file1.txt dir

# copy mutiple files to existing directory
cp file1.txt file2.txt dir

# copy file to existing directory which already has copying file :: use interactive option to pop up prompt
cp -i file1.txt file2.txt dir

# copy directory to another directory
1) when dir3 directory not exists
cp -R dir1 dir3 :: It will just copy contents in dir1
e.g) cp -R dir1 dir3
ls -al dir3 :: list1.txt list2.txt aaa

2) when dir3 exists
cp -R dir1 dir3 :: It will copy dir1 as sub directory of dir3 and its contents.
e.g) cp -R dir1 dir3
ls -al dir3 :: dir1/list1.txt list2.txt aaa

```

## mv
```bash
# move file1.txt to file2.txt (if file2.txt not exsits, file1.txt will be renamed to file2.txt, if exists, overwrites it )
mv file1.txt file2.txt

# move file to existing directory which already has a same name file :: user interactive option 
mv -i file1.txt dir1

# show extra info
mv -v file1.txt file2.txt

$ move directory1 to directory2
1) when directory2 not exists
mv dir1 dir2 :: just move contents
2) when directory 2 exists
mv dir1 dir2 :: dir1 is copied as a sub directory to dir2
```

## less
```bash
# Used to read a file or find some contents inside a file like pattern or words

# read a file
less file1.txt

# go up and down using up and arrow key

# use space bar to go to next page

# to go to next page reverse :: press b

# go to first of page :: press g

# go to last of page :: press shift+g

# find content :: /xxx + enter + press n

# find content reverse :: ?xxx + enter + press n
```

## touch
```bash
# create an empty file
# change the timestamp if touched file already exists
```

## sudo and sudoers
```bash
# basic command
sudo ls /home/ryan

# how to switch to root user
sudo su -

# how to switch to different user
su XXX

# how to edit sudoers file 
# Must edit the sudoers file using visudo command and if there are more than2 grammatical errors, it will lock all  users and recover process will be quite difficult.
sudo visudo -f /etc/sudoers

root        ALL = (ALL) ALL
%admin      ALL = (ALL) ALL // % => group

# by Adding user to admin group, added user can be elevated to super user using sudo command
# To look in specific (admin in here) group
grep "admin" /etc/group

# Add user(smith) to admin group
sudo adduser smith admin // evn though I changed to root user using "su -", it show error "adduser command not found." ???

# Delete user in admin grup
sudo deluser smith admin // same command not found error. ask someone!
```

## top
```bash
# Check cpu, memory status, process id ....
```

## ps
```bash
# Display all process
```
```bash
# Display current user proces
ps -ux (ps ux)

# Display all users process
ps -aux (ps aux)

# Display specific user process
ps -U ryan

# Display instances or post process of gnome-terminal
ps -C gnome-terminal
```

## find
```bash
# search for files in directorial hierachy
```
```bash
find /etc -name test.sh
find /etc/shell -name xxx.*

# find files in sub directories
find . -print | grep -i foo

# find files which are created 1 day ago
find /home/programming/ -mtime -1
```

## grep( global regular expression print )
```bash
# Print any line which matches specified pattern
```

```bash
# Find "options" in file.txt ignoring case
grep -i "options" file.txt 

# Find "options" in file.txt with line number
grep -n "options" file.txt

# Find "options" in multiple files
grep -n "options file.txt file2.txt file3.txt
OR
grep -n "options" *

# Find all lines which do not contain "options" pattern (v = invert match)
grep -nv "options" file.txt
```

## .bashrc (.zshrc in zshell)
```bash
# Script that is executed whenever new session is started in interactive mode.
# Located in home directory
```
