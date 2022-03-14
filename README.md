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
* Wild card
	* ls $dir/[a-c]* - Starts with a, b, or c
	* ls /bin/[a-c]*t - Starts with a-c and ends with t
	* ls /bin/[a-c]*[te] - Starts with a-c and ends with te
	* ls /bin/[!a-c, m-z]* - Does not start with a-c
* cd - goes to home director, cd .. - goes to previous directory
	* cd /sc/arion/projects/
* man ls - goes to the manual page
	* Inside man page type / to search for specific words
	* ls --help - better command to easily access command switches
	* Press Space, or Enter to navigate
* ln - link command
	* ln -s <path-to-file> <path-to-link - default home directory>
	* ln -s ~/play2/hello.txt /hpc/users/babupk01/
		* s - symbolic link which is not a hard link
		* ○ -> ALIAS - soft link
* mkdir
	* mkdir ~/play2 - makes a directory called play2 in the home directory
	* mkdir -p - parent - if previous directory doesn't exist it creates them, and also it wont throw up an error if directory already exists
* rmdir
* rm <file-name>
	* rm -r <folder-location>
	* -r - recursive
	* -f - force
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

# User related
	
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
.bashrc -> ~/.bashrc

* https://unix.stackexchange.com/questions/129143/what-is-the-purpose-of-bashrc-and-how-does-it-work
	
.bash_profile ->	

If .bashrc not running when starting a new terminal, then make the following changes to your .bash_profilehttps://askubuntu.com/questions/161249/bashrc-not-executed-when-opening-new-terminal

## Bash Shell Keyboard Shortcuts (http://www.keyxl.com/aaaf192/83/Linux-Bash-Shell-keyboard-shortcuts.htm)

* Ctrl + U	Clears the line before the cursor position. If you are at the end of the line, clears the entire line.
* Ctrl + R	Let's you search through previously used commands
* Ctrl + C	Kill whatever you are running
* Ctrl + D	Exit the current shell
* Ctrl + Z	Puts whatever you are running into a suspended background process.
* fg - Resumes job that was suspended
* bg - sends process to background
* Ctrl + W	Delete the word before the cursor
* Ctrl + K	Clear the line after the cursor
* Tab	Auto-complete files and folder names
* Ctrl + Y : Restores the lately removed with Ctrl + W or Ctrl + U or Ctrl + K text
* q Quits man page
* Spacebar - Bigger movement through the manpage compared against Enter

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

## wget

wget miniconds_download_link.sh
bash miniconds_download_link.sh
wget ftp://ftp.broadinstitute.org/outgoing/lincRNA/ABC/AllPredictions.AvgHiC.ABC0.015.minus150.ForABCPaperV3.txt.gz

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

Tee

Command I/O - UNIX has special names for the output and input of commands
* Standard In - STDIN - 0
* Standard Out - STDOUT - 1
* Standard Error - STDERR - 2
* Pipe redirects the STDOUT to STDIN of another command
	* env | grep USER
	* env contains many variables, we are extracting the USER variable using grep
	* outputs each line that matches the input parameter to STDOUT
	* If the line contains an invalid character, output goes to STDERR

grep <expression_to_match>
* -v - invert match, selects the line that don't match

Redirects - pipe that sends output to a file (file descriptors - file descriptor number or file name) rather than a command
* All three input, output types can be redirected
	* STDOUT redirect is >, which is equivalent to 1>
	* STDIN redirect is <
	* STDERR redirect is 2>
	* Redirects can be combined with the & sign
		* >2&1> send STDERR to where STDOUT is going

Programs have file descriptors too [source_descriptor_file] redirect_option [destination_descriptor_file]
* < opens file descriptor to read
* > opens file descriptor to write
* >> opens file descriptor to append

Stream editor - Changing text 'on the fly'
* grep aaaaaaaa database.dat  | sed 's/aaa/xxx' > database_modified.txt
* diff database.dat database_modified.txt
* grep aaaaaa database.dat | sed 's/a/x/g' > database_modified_2.txt
* diff database.dat database_modified_2.dat
* cat database.dat | sed '/aaaa/d' > database_modified_3.txt
* diff database.dat database_modified_3.dat

Packing files (tar) - originally meant tape archive
*   tar -cf archive.tar foo bar  # Create archive.tar from files foo and bar.
*   tar -tvf archive.tar         # List all files in archive.tar verbosely.
*   tar -xf archive.tar          # Extract all files from archive.tar.

Compressing files (gz - stands for gnu-zip)
* gzip database.dat
* ls database* (* is wildcard - used to find database.dat.gz)
* gzip -d database.dat.gz - to uncompress the compressed file

* cal 7 1997 - shows the calendar of July 1997

sh - shell - is a command line interpreter that executes command read from a command line string, the standard input or a specified file.

Subshells
* They are like a function, the variables defined within these parentheses are local variables
i.e., the "scope" of the variable is limited, a global variable on the other hand can be accessed both 
within the subshell as well as outside the subshell.

```
#!/bin/bash
XD=1
(YD=2 echo $XD $YD)
echo $XD $YD
```

So, the output for the above script will be

	
1 2
1

There are several ways to create subshells
* Using parentheses () - Output is sent to STDOUT
* Using backtick characters `` - the command inside is replaced with output from Shell
* Using $() - command is changed into an unnamed variable
* Using <() - command in changed into a virtual file, and returns the file name

## Process substitution
* A subshells output can be captured and used as an input using the pipe operator
* This process of capturing the output is called process substitution because we are using a "process" as a "substitute" for a variable or file.

## Commands and outputs
* (echo $USER) : babupk01
* echo $USER : babupk01
* echo $(USER) : will throw an error
* echo `which env` : /usr/bin/env
* echo (which env) - will throw an error
* echo $(which env) - /usr/bin/env
* echo < which env - will throw an error
* echo < (which env) - will throw an error
* echo <(which env) : /dev/fd/63
* echo < $(which env) - will print an empty line
* grep USER <(env) : USER=babupk01
* grep USER <(env) : USER=babupk01
* grep USER < (env) - throws an error
* env | grep USER : USER=babupk01
* echo $(date) : shows today's date, which is the same output as the command date
* echo "date": prints date
* echo "date" | sh : send output of echo "date" to shell script
* echo "date" > datescript : Writes date to a file called datescript
* sh datescript : prints the date
* cat datescript | sh : prints the date

# Why ldd `which env` and why not which env | ldd ?
Pipe sends the output of which env to the input of ldd, but ldd needs a parameter not an input.

# Why env | grep USER and why not grep USER `env` ?
grep USER `env` translates to grep USER env_command_output which doesn't make syntactic sense.
Pipe'ing' output of env STDOUT as input to grep USER seems to work. 

## Quotes
* " " - evaluates variables in between them and then returns the output
* ' ' - echos whatever is within the quotes
* `` - Executes the command

## Shell scripting
* Every scripting file begins with this
	* When a script file is executed, the file is being called as an application, as if it was a binary file
	* The shell checks the type of application, and how to run it - "file magic"
	* The shebang line is the first line a script that makes it self executable
	* #/usr/bin/env python - is used to specify to shell that it is a python application
	* #!/bin/bash or #!/bin/csh -is used to specify to shell that it is a binary application
	* A file that contains a set of shell commands
	* Equivalent of a source file that is used in R
		* So consider it like a function, which we use to reduce code repetition
	* Comments can be used in shell scripts using the # symbol

## Execution
* Each shell script executes a new shell program i.e., a "child process"
	* All processes start from the current process, then "fork" into "child processes", e.g. scripts
	* Every process gets a process ID, or PID, which is accessed using the $$ sign
	* Child shell inherits exported variables 
		* Variables inside child shell do not change parent shell variables 
	* So, it has its own set of variables, which doesn't contain the variables in the "parent process"
	* To use a variable from the parent process in the child process, we use the command export

## Multi-user environment
	* Each person's shell can be configured differently, with different environments pointing to different PATHs
	* This is different from a normal GUI. Each app is installed in its own big disk space on folder, not in a common folder.
	* In case one wants to use a different PATH or LD_LIBRARY_PATH
		* export PATH=''$PATH
		* export LD_LIBRARY_PATH='' 
	* But how do you keep track of which program requires which package?
		* Minerva uses what is called "Environment modules" to deal with this
		* Module files define the path to specific apps, and all of their dependencies
		* Module files also change the environment based on the need of the particular program being run
	* module avail - lists all the module in the system to STDERR
	* module list - lists all the modules currently loaded
	* module load X - loads a particular module X
	* module unload X - unloads a particular module X
	* module purge - unloads all modules

sleep 5 - delays the process for five seconds
ps - returns a current snapshot of the processes
	
## Scripts vs compiled language
	
* Script contain instructions for another program to interpret, and execute some function built into that program
	* Quick to write/debug
	* Easily modifiable
	* Does not scale well
	* Limited to simple constructs (loops, conditionals)
	* E.g., Shell script (bash, csh, ksh, …), R, Matlab, Python

printenv - print the values of the specified environment variable
printf - format and print data

## Source
	
Executes command as if they were terminal input, so the CV (Child variable) is accessible outside of the shell script.

## For loop - semi colon stands for new line
	
SYNTAX: for NAME [in LIST]; do COMMANDS [$NAME]; done
[in LIST] is optional if not given it is replace by $@ which stands for all shell arguments e.g. $1, $2, $3, …
$1 is the argument of a shell call.

{START..END}

{START..END..INCREMENT}

Indentation helps
	
Arithmetic

Not preferred way of updating variables
	
Preferred way of updating variables

Counting

Bitwise operators work on bits, and make bit by bit operations
Logical operators work on making a decision based on multiple conditions

screen
* Starts a command line session that you can detach from and then re-attach to from the same or another computer.
* Each session is preferably given a name
* Disconnect by using ^A^D
* screen -s mysession
* screen -s count1
* ./count.sh
* screen -r mysession
* screen -ls
* You can always log in to a new window, and start a second job there, instead of using a screen
	
shuf
* Shuffle or permute randomly

file - determines file type

To count the number of files

wc - print newline, word, and byte counts for each file
* -l - prints the newline counts
* -c - prints byte counts
* -m - prints character counts
* -L - prints length of the longest line
* -w - prints word counts
	
Backgrounding multiple tasks

Shell variable RANDOM is a random number between 0 and 32767

What did $1 or the lack of parameters mean?


wait command which pauses until execution of a background process has ended.

Where are the files? The files are being generated by bg.sh and being stored in ~
What change in the script would make the files show? 
nohup, start in background

nohup - no hang up - ignore the hang up signal
hup is the way terminal warns dependent processes of logout

A program will gets the following command, terminates.


This is used to safely log off, but the job will keep running in the background.

If, then conditions, logical testing

Syntax: IF <TEST_COMMANDS>; then <TEST_COMMANDS>;fi
TEST is a command to evaluate a logical expression
	• [ ] - synonym for TEST
	• [[ ]] - new and improved TEST



Also, in bash, success (TRUE) = 0, failure (FALSE) = 1
Return status is the exit status of the last command or 0 if the condition tested TRUE

Difference between && and ||, && executes if previous command exited with 0, || executes if previous command exited with 1
-eq - equal to
-ne - not equal to
-lt - lesser than
-le - lesser than or equal to
-gt - greater than
-ge - greater than or equal to

Issue: If a file is both ASCII and an executable, then it won’t be counted as an executable. 

But there is a fix. (if_fx.sh) Check slides, when you are not brain dead, and are capable of processing information. 

While loop

Until loop

Go through count_n.sh

dos2unix - to convert a Windows DOS file to a Unix file. Windows uses CR LF to end lines, whereas Unix just uses an LF. CR LF refers to carriage return - moves the cursor without advancing to the next line. Unix uses line feed, which moves the cursor down to the next line without returning to the beginning of the line

bjobs - The LSF scheduler system 

awk - an interpreted programming language typically used for data extraction, it is not a part of bash. Intent of creating this language, was to write single line aka in-line programs.
* awk [options] -f scriptfile file
* If match occurs, then the action is taken per line
* awk [options] in-line-program file
	* awk '/attccagaacatttccatcaccccgaaaagaaaaccctaaatcctttatc/ {print}' database.dat
* $0 - Entire record/line
* $1, $2, …, $NF are fields
* NR is the record/line number working on

wc
sed -n '/gtgggggaaccttccagaaagaggcaacatcatgtgctaaggtcccaggt/p' database.dat



	
