# bash_lookup

Useful bash cheatsheet

Look up explainshell.com to get more information on specific commands, and command switches

# Basics

* drag and drop file into Shell - will give you the directory of the file
* pwd
* ls -lah
	* l long listing
	* a hidden files
	* h human readable
	* dir=/hpc/packages/minerva-common
* Wild card
	* ls $dir/[a-c]* - Starts with a, b, or c
	* ls /bin/[a-c]*t - Starts with a-c and ends with t
	* ls /bin/[a-c]*[te] - Starts with a-c and ends with te
	* ls /bin/[!a-c, m-z]* - Does not start with a-c
* cd - goes to home director cd .. - goes to previous directory
	* cd /sc/arion/projects/
* man ls - goes to the manual page
	* Inside man page type / to search for specific words
	* ls --help - better command to easily access command switches
* ln - link command
	* ln -s <path-to-file> <path-to-link - default home directory>
	* ln -s ~/play2/hello.txt /hpc/users/babupk01/
		* s - symbolic link which is not a hard link
		* ○ -> ALIAS - soft link
* mkdir
	* mkdir ~/play2 - makes a directory called play2 in the home directory
* rmdir
* rm <file-name>
	* rm -r <folder-location>
* cp -r <folder-location> <destination>
	* cp /sc/arion/projects/BMI1005/liglib/*.mol2 .
		* . refers to here, not the home directory
		* if you want to copy it to home, replace . with ~
		* .. refers to the directory just above the current directory
		* Wildtype character - * matches everything with .mol2 
* cat <file-name> - prints all contents of file to screen
* head <file-name> -n 10 - prints first 10 lines of file to screen
* tail <file-name> -n 10 - prints last 10 lines of file to screen
* less <file-name> - interactively go through file
* more <file-name> - interactively go through file
* clear - clears screen

# User
	
* w <username> - shows currently logged in users, and what are they doing
	* w babupk01
* finger <username> - can look up user specific information
	* finger -lmsp babupk01
		* -l - multi-line format
		* -m - prevents matching of user name to other names, just uses the login name
		* -s - display's user's login name, real name, terminal name, write status, idle time, login time, office location and office phone number
		* -p - doesn't display plan information
* id - gives you your information regarding the user, group and others
	
# File usage
	
* df <file-directory-destination> gives file system disk usage stats
	* file system, %disk used etc
* df -h /sc/arion/
* du <path-directory> <optional - can give name of directory> -hs, -h human readable, -s is summarizing
	* estimate disk usage for specific groups of files or directories
	* basically gives disk usage for each file and directory in path

# Other
	
* sort - sort lines of text files
	* -g - general numeric sort
	* -r - sort by reverse order
	* -n - compare according to string numeric value
	* -u - unique
	* -k - sort via a key
		* Unix indexing starts from 1, blank is a separator, unlike cut
* uniq - report or omit repeated lines
	* -c - count - prefix lines by number of occurrences 
	* -d - only print duplicated lines - one for each group
	* -u - only print unique lines
* who am i
	* am i == -m command switch
	* who | sort -k 2 --sort=Random | tail -n 10
* date - prints system date and time
	* +%s - seconds since
* echo <string>
	* prints string
	* echo -e ${PATH//:/\\n} - prints PATH line by line 
		* -n - do not output the trailing newline
	* echo $! - gives process ID of last submitted process
	* echo !$ - gives the last used argument
* kill <PID> - Kills a given process
	* kill $! - kills the latest process or the last PID
	* -9 - if kill does not work add this command switch
* cut - remove sections from each line of a file
	* -d delimiter
	* -f selects only the specified field
* env - gives details regarding the environment in which UNIX runs
	* env | less
	* Provides a interactive way of going through env
	* Before filename was the parameter to less, now it’s the pipe output

## BasH files
	
.bash_history -> keeps a list of the previous commands
.gitconfig -> repository/coastal-personal-home/.gitcconfig
.bashrc ->	
.bash_profile ->	
	
## Bash Shell Keyboard Shortcuts (http://www.keyxl.com/aaaf192/83/Linux-Bash-Shell-keyboard-shortcuts.htm)

Ctrl + U	Clears the line before the cursor position. If you are at the end of the line, clears the entire line.
Ctrl + R	Let's you search through previously used commands
Ctrl + C	Kill whatever you are running
Ctrl + D	Exit the current shell
Ctrl + Z	Puts whatever you are running into a suspended background process.
fg - Resumes job that was suspended
bg - sends process to background
Ctrl + W	Delete the word before the cursor
Ctrl + K	Clear the line after the cursor
Tab	Auto-complete files and folder names
Ctrl + Y : Restores the lately removed with Ctrl + W or Ctrl + U or Ctrl + K text
q Quits man page
Spacebar - Bigger movement through the manpage compared against Enter

# Variables
 
* $USER 
* $PWD 
* $LD_LIBRARY_PATH - path to library - pieces of code with lots of standard functions 
* $PATH - variable with locations where shell commands exist 
	
* Variable names are in CAPS
* Variables are set as follows VARIABLE_IN_CAPS="This is the assigned value"
	* No space should be given before and after the equal sign
	* Variable type matters
* Variables can be printed as follows echo $VARIABLE_IN_CAPS
* Quotes may be needed to call variables
* which <shell_command> locates the executable file associated with the given command by searching it in the $PATH environment variable
	* which ls
* ldd - prints shared objects(libraries) required by each program or shared object specified
	* ldd /bin/env

## Understanding ls -l long listing
	
* First - is to mention if it is a directory, it is d if it is, else it is just -
	* Next set of three - are to specify the file permission for Owner
	* Next set of three - are to specify the file permission for Group
	* Next set of three - are to specify the file permission for Others
		* r - read
		* w - write
		* x - execute
		* l - symbolic link
		* b - block special file
		* c - character special file
		* p - pipe special file
		* s - local socket special file
* chown - to change owner of file - requires sudo permission
* chgrp - to change group with which file is associated with - requires sudo permission
* chmod (a|g|u) (+|-) (r|w|x) <file | directory name>
	* chmod 700 ./play2 - gives rwx permissions to user, and no permission to group and others
	* OR chmod 751 <file | directory name>
	* a - all, g - group, u - user
	* + - add access, - - remove access
	* read is 4 points, write is 2 points, execute is 1 point
* We can traverse (cd) to a folder if we have executable access, then if they have read access they can read the contents of the folder
	* Changing the permissions to a folder doesn't the alter the permissions to the contents of the folder

# Access Control Lists

* ACL - Access Control Lists
	* Allows you to set arbitrary permissions for any group or user on a file
	* setfacl -m user:krishr12:rwx database.dat - I am giving krishr12 the permission to read, write and execute database.dat
	* setfacl -r to assign permission to an entire directory
* FACL - File system Access Control Lists
	* getfacl database.dat - gets proper details on who the user is, who the group is, what are their permissions.

## linebreak

\ allows line break without breaking the command
env \
| grep USER


## .bashrc and .bash_profile

If .bashrc not running when starting a new terminal, then make the following changes to your .bash_profilehttps://askubuntu.com/questions/161249/bashrc-not-executed-when-opening-new-terminal

## wget

wget miniconds_download_link.sh
bash miniconds_download_link.sh

## diff

Following is a linux command to look at differences between 2 files, 
helps a lot when you want to compare two different versions of a file

The -y command switch, shows the differences between the two files column-wise.

```
diff file1.txt file2.txt -y
```
It shows the changes that need to be made in file 1 to become file 2.
Or put another way, it shows the differences between file 1 and file 2, with respect to file 1. 

The format in which it shows the difference is as follows: >File1LineNumber{add (a),change (c), delete(d)}File2LineNumber
Eg: 1a2, means add line number two from file 2 after file 1 

## split and cat

Uploading files of size > 1 GB to the server using remote access is difficult. So, instead large files can be split into smaller files, uploaded to server and then merged.

```
split -b 200m _CellRangerOutput_matrix.mtx cellRanger_segment.mtx
cat cellRanger_segment.mtx* > _CellRangerOutput_matrix.mtx
rm cellRanger_segment.mtx*
```

# Vim

* I - Insert mode
* :set paste - goes to insert paste mode - ctl + shift + v - Can copy, paste and edit
* set !paste - unsets paste

# Minerva

* /hpc/users/babupk01 - Home directory ~20GB
* /sc/arion/work/babupk01 - Work directory ~100GB
* /sc/arion/scratch/babupk01 - Scratch directory Unlimited but 2 weeks
* /sc/arion/projects/BMI1005 - Project directory
* /sc/arion/scratch/mezeim01/BMI1005 - Backup
* /sc/arion/ & /hpc/users/ are called mount points
	
# Pipe

* Output of one command is the input to the other
* Output of one command determines the input parameters of other command
* One command generates a command which is run
* Can encapsulate a set of commands and give it to a script to run
	* echo $PATH | cut -d: -f2




	
