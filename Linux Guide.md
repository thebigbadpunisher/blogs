## In this Linux command line cheat sheet, we will learn:
-   Basic Linux Commands
-   File management user management Linux Commands
-   Programing Linux Commands
-   Job management Filesystem management Linux commands
-   Process management Linux Commands
-   Shortcuts
-   network
-   System Info
-   Searching
-   File Permission

### Basic Linux Commands
-   cat – Joins and displays files
-   cp – Copies files
-   cpio – Creates an archive, restores files from an archive, or copies a directory hierarchy
-   cut – Selects characters or fields from input lines
-   diff – Displays the differences between two text files
-   emacs Editor
-   expand – Converts TABs to SPACEs
-   find – Finds files based on criteria
-   grep – searches for a pattern in files
-   gzip – Compresses or decompresses files
-   head – Displays the beginning of a file
-   join – Joins lines from two files based on a common field
-   less – Displays text files, one screen at a time
-   ln – Makes a link to a file
-   ls – Displays information about one or more files
-   man – Displays documentation for utilities
-   mkdir – Creates a directory
-   mv – Renames or moves a file
-   nl – Numbers lines from a file
-   od – Dumps the contents of a file
-   paste – Joins corresponding lines from files
-   rm – Removes a file (deletes a link)
-   sed – Edits a file noninteractively
-   sort – Sorts and/or merges files
-   split – Divides a file into sections
-   tail – Displays the last part (tail) of a file
-   tar – Stores or retrieves files to/from an archive file
-   touch – Creates a file or changes a file’s access and/or modification time
-   uniq – Displays unique lines from a file
-   vim Editor
-   wc – Displays the number of lines, words, and bytes in one or more files

### File management user management Linx Commands
-   cd – Changes to another working directory
-   chgrp – Changes the group associated with a file
-   chmod – Changes the access mode (permissions) of a file
-   chown – Changes the owner of a file and/or the group the file is associated with
-   date – Displays or sets the system time and date
-   df – Displays disk space usage
-   dmesg – Displays kernel messages
-   du – Displays information on disk usage by directory hierarchy and/or file
-   finger – Displays information about users
-   kill – Terminates a process by PID
-   killall – Terminates a process by name
-   nice – Changes the priority of a command
-   nohup – Runs a command that keeps running after you log out
-   ps – Displays process status
-   renice – Changes the priority of a process
-   sleep – Creates a process that sleeps for a specified interval
-   stat – Displays information about files
-   stty – Displays or sets terminal parameters
-   sysctl – Displays and alters kernel variables at runtime
-   top Dynamically displays process status
-   umask Specifies the file-creation permissions mask
-   w Displays information about local system users
-   which Shows where in PATH a utility is located
-   who Displays information about logged-in users

### Programing Linux Commands
-   configure – Configures source code automatically
-   gawk – Searches for and processes patterns in a file
-   gcc – Compiles C and C++ programs
-   make – Keeps a set of programs current
-   mawk – Searches for and processes patterns in a file
-   perl – Scripting language
-   python – Programming language

### Job management Filesystem management Linux commands
-   at – Executes commands at a specified time
-   cal – Displays a calendar
-   crontab – Maintains crontab files
-   echo – Displays a message
-   expr – Evaluates an expression
-   fsck – Checks and repairs a filesystem
-   mkfs – Creates a filesystem on a device
-   screen – Manages several textual windows
-   tee – Copies standard input to standard output and one or more files
-   test – Evaluates an expression
-   tr – Replaces specified characters
-   tty – Displays the terminal pathname

### Process management Linux Commands
-   bg – To send a process to the background
-   fg – To run a stopped process in the foreground
-   top – Details on all Active Processes
-   ps – Give the status of processes running for a user
-   ps PID – Gives the status of a particular process
-   pidof – Gives the Process ID (PID) of a process
-   kill PID – Kills a process
-   nice – Starts a process with a given priority
-   renice – Changes priority of an already running process
-   df – Gives free hard disk space on your system
-   free – Gives free RAM on your system

### Shortcuts

-   Ctrl+C – halts the current command
-   Ctrl+Z – stops the current command, resume with
-   fg in the foreground or bg in the background
-   Ctrl+D – log out of current session, similar to exit
-   Ctrl+W – erases one word in the current line
-   Ctrl+U – erases the whole line
-   Ctrl+R – type to bring up a recent command
-   !! – repeats the last command
-   exit – log out of current session

### Network

-   ping host – ping host and output results
-   whois domain – get whois information for domain
-   dig domain – get DNS information for domain
-   dig -x host – reverse lookup host
-   wget file – download file
-   wget -c file – continue a stopped download

-   ./ – curret directory right now
-   ../ – previous directory
-   ~ – the users home directory
-   | – pipe the output of one command into another
-   > – use command on the following file (overwrite)
-   >> – use command on following file (appends)

### Compression

-   tar cf file.tar files – create a tar named file.tar containing files
-   tar xf file.tar – extract the files from file.tar
-   tar czf file.tar.gz files – create a tar with Gzip compression
-   tar xzf file.tar.gz – extract a tar using Gzip
-   tar cjf file.tar.bz2 – create a tar with Bzip2 compression
-   tar xjf file.tar.bz2 – extract a tar using Bzip2
-   gzip file – compresses file and renames it to file.gz
-   gzip -d file.gz – decompresses file.gz back to file

### System Info

-   date – show the current date and time
-   cal – show this month’s calendar
-   uptime – show current uptime
-   w – display who is online
-   whoami – who you are logged in as
-   finger user – display information about user
-   uname -a – show kernel information
-   cat /proc/cpuinfo – cpu information
-   cat /proc/meminfo – memory information
-   man command – show the manual for command
-   df – show disk usage
-   du – show directory space usage
-   free – show memory and swap usage
-   whereis app – show possible locations of app
-   which app – show which app will be run by default

### Searching

-   grep pattern files – search for pattern in files
-   grep -r pattern dir – search recursively for pattern in dir
-   command | grep pattern – search for pattern in the output of command
-   locate file – find all instances of file
-   find /dir/ -name name* Find files starting with name in dir
-   find /dir/ -user name Find files owned by name in dir
-   find /dir/ -mmin num Find files modifed less than num minutes ago in dir

### File Permissions

-   chmod octal file – change the permissions of file to octal, which can be found separately for user, group, and world by adding
-   4 – read (r)
-   2 – write (w)
-   1 – execute (x)

### IO Redirection

-   cmd < file Input of cmd from file
-   cmd1 <(c  
    md2) Output of cmd2 as file input to cmd1
-   cmd > file Standard output (stdout) of cmd to file
-   cmd > /dev/null Discard stdout of cmd
-   cmd >> file Append stdout to file
-   cmd 2> file Error output (stderr) of cmd to file
-   cmd 1>&2 stdout to same place as stderr
-   cmd 2>&1 stderr to same place as stdout
-   cmd &> file Every output of cmd to file