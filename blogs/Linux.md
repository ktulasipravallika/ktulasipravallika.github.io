### Linux 

* Linux is an open-source kernel responsible for managing hardware resources such as CPU, memory, devices, and processes.
* The kernel manages CPU, memory, devices, and provides system calls to user space.
* A complete Linux operating system is formed when the kernel is combined with user-space components like GNU libraries, shell utilities, system services, and package managers.
* The Linux kernel has five core responsibilities:
   * Process Management
      * Creating processes (fork)
      * Scheduling (which process runs on CPU)
      * Context switching
   * Memory Management
      * Allocating and freeing RAM
      * Virtual memory
      * Paging and swapping
   * Device Management
      * Communicates with hardware via device drivers.
      * Abstracts hardware details from user programs.
   * File System Management
      * Handles files, directories, permissions.
      * Interfaces with filesystems like ext4, xfs.
   * System Call Interface
      * Provides a secure interface between user space and kernel space.
      * Examples: read(), write(), open(), fork()

### Kernel Space vs User Space

Kernel space runs privileged code, user space runs applications, and system calls act as the controlled bridge between them.

#### **Kernel Space**

   * Where the **Linux kernel runs**.
   * Has **full access** to hardware. (CPU, memory, devices)
   * Executes **privileged instructions**.
   * A bug here can **crash the entire system**.
   * Examples: 
      * Process scheduler
      * Memory manager
      * Device drivers
      * Filesystem code

#### **User Space**

* Where **applications run**.
* Has **restricted access**.
* Cannot directly access hardware.
* Must request services from kernel.
* Examples:
   * Shell (`bash`)
   * Commands (`ls`, `ps`, `grep`)
   * Applications (databases, web servers).
   * Docker, Java, Python programs.
* `ls` command runs in user space because it is a regular user program. When it needs information (like directory contents), it makes system calls to the kernel, which then accesses the filesystem and returns the results.

### System Call

* A system call is a controlled interface that allows a user-space program to request services from the kernel, such as accessing files, memory, processes, or devices.
* User programs cannot directly access hardware.
* Kernel protects the system from unsafe operations.
* System calls provide a safe boundary.
* Examples of System Calls :
   * open() → open a file
   * read() → read from file or device
   * write() → write data
   * fork() → create a process
   * exec() → run a program

* When you type `ls` and press Enter:“The shell forks a process, the child execs `ls`, `ls` uses system calls to read the directory, prints output, exits, and control returns to the shell.”

### FileSystem and Navigation

* `/` → The top-level directory of the filesystem. Everything in Linux starts from /.
* `/etc` → Stores system-wide configuration files.
* `/var` → Stores variable data that changes over time like var/logs/syslog, /var/log/messages, /var/log/auth.log 
* `/usr` → Stores user-space programs, libraries, and binaries.
* `/home` → Contains home directories for users, where personal files live.

### File Permissions

* Permissions are applied to three categories:
   * Owner (User)
   * Group 
   * Others
     
* Permissions
   * `r` means read
   * `w` means write
   * `x` means execute

**Note** :
  * Execute on a directory → ability to enter it.
  * Read on a directory → ability to list files.

### Users

**Linux user** :
  * A Linux user is an account that represents a person or service interacting with the system, identified by a user ID (UID) and used to control permissions and access.

**Root User** : 
  * The root user is the superuser with unrestricted access to the entire system.
  * UID is 0.

**Sudo** :
  * `sudo` allows a regular users to execute specific commands with root (superuser) privileges, based on permissions defined in the system.
  * sudo actions are logged in `/var/log/auth.log`.
  * Uses:
    * Improves security.
    * Provides audit logs.
    * Limits who can run what.
    * Reduces accidental system damage.
  * `/etc/sudoers` → defines which users or groups are allowed to use `sudo` and what commands can they run.
  * `visudo` → Opens the file which consists details about sudo users.

### Groups

**Linux Group** :
  * A Linux Group is a collection of users used to manage permissions and access to files and resources collectively.

**Primary Group:**
  * A primary group is the main group associated with a user and is used by default when the user creates files.

**Secondary Group:**
  * Secondary (supplementary) groups are additional groups that grant extra permissions to the user.
    
### Process

* A **Process** is an instance of a program in execution with its own memory, CPU, state and process ID(PID).
* Process is an independent running program.
* It is more expensive to create and switch and is isolated form other processes.
  * Example :
    * ngnix
    * mysql
    * python file.py
      
* **Parent Process** : 
  * A parent process is the provcess that creates another process using fork().
    
* **Child Process** :  
  * The newly created process after fork() is child process.
  
**Example** : When a shell runs ls, the shell is the _PARENT_ and ls runs as the _CHILD_ process.

* **Orphan Process** :  
  * If the parent process terminates, the child process become the _ORPHAN_ process.
  * This process is adopted by the init/systemd process(PID 1).
  * This child process(Orphan process) still keeps running (DO NOT automatically terminate)

* **Zombie Process** :
  * A zombie process is a process that has finished execution, but still has an entry in the process table.
  * A child process exits, but the parent process doesnot call wait().
  * At this stage kernel keeps minimal info about this process like PID and exit code.
  * Zombie process cannot be killed because it is alreday dead and it disappears only when parent reaps it using wait().
    
    * **wait():**
      
      * **General flow** : Parent fork() →  Child → Child exits → Parent calls wait() → Kernel removes child from process table → No zombie.
        
      * **Zombie process** : Parent fork() → Child → Child exits → Parent never calls wait() → Zombie process remains.
        
  * To fix Zombie Process :
    *  Kill or restart the parent process
    *  Parent must call wait()
    *  Reboot (last resort) 
    
### Program

Program is a file on disk.

### Thread

* A thread is a light weight unit of execution inside a process.
* Thread share the same memory and are faster to create.
* If a thread crashes, it can bring down the entire process, because threads share the same memory space.
  * Examples:
    * Java threads
    * Python threads
   
### Memory Management

* **RAM** : Random Accesss Memory
  *  RAM is volatile memory that holds running programs, processes, and data required by the CPU for fast access.
  *  Its contents are lost when the system is powered off.
  *  RAM is System memory.

**Swap Memory**
  *  Swap is disk space used to extend RAM and prevent memory exhaustion when physical memory is full.
  *  When both RAM and Swap are fully used, the Linux kernel invokes the OOM Killer (Out-Of-Memory Killer), which forcefully terminates one or more processes to free memory.

### CPU & Load

**CPU Usage**:    
  * CPU Usage is the number of processes actively executing/running on the CPU.
    
**CPU Load** 
  * CPU load indicates the number of processes that are either running on the CPU or waiting to run.

**Load Average** 
  * Load average is average number of proceses that are running or waiting for CPU over a period of time (1 Minute, 5 Minutes, 15 Minutes).

### Files, Directories and Logs

**Files** : 
  * A file stores data, such as text, scripts, or binaries.
    
**Directories** :
  * A directory is a container that holds files and other directories.

**Paths** :
  * **Absolute Path** → /home/ubuntu/projects (starts from /)   
  * **Relative Path** → projects  # relative (from current directory)               

### Netwroking Basics

**DNS : Domain Name System**
* Translate the human readable domain names into IP addresses so systems can locate each other on a network.

## Commands

* `#!/bin/bash` → Shebang
* `./file_name` →

#### Users and Groups

* `cat /etc/passwd` →
  
* `cat /etc/group` →
  
* `useradd user_name` →
  
* `userdel user_name` →
  
* `groupadd group-name` →
  
* `groupadel group-name` →
  
* `groups user_name` →
  
* `id user_name` →
  
* `sudo -l` → Fast way to confirm “do I have the rights to restart services, read logs, change firewall rules, etc.?” during troubleshooting.

* `whoami` → Prints the effective username of the current process.

#### Process Commands

* `top`
  * Shows running processes, continuously updating the process information.
  * Real-time CPU & memory usage.
  * Better for live debugging.
  
* `htop`
  * Provides colored output and Mouse support.
  * Tree view of processes and Easier killing & filtering

* `ps`
  * Shows the snapshot of processes running at a specific moment. 
    * `ps -ef` → Focuses on CPU/memory usage.       {`-e` → Every Process, `-f` → Full Format}
    * `ps aux` → Emphasizes process hierarchy and parent-child relationships.      {`a` → all users `u` → user oriented format `x` → include processes without terminal}
      
* `kill`
  * `kill process_id`
     * Allows the process to clean up resources, close files and save state.
     * Sends signal to terminate and lets process handle the teermination.
     * `TREMINATE GRACEFULLY` (signal is called `SIGTERM`)
       
  * `kill -9 process_id`
     * Kernel immediately kills the process
     * No cleanup is performed.
     * Cannot be ignored
     * `TREMINATE FORCEFULLY` (signal is called `SIGKILL`)

  * `pkill process_id` 

#### Disk and File Systems

* `df -h`
  
* `du -sh /*`
  
* `mount`
  
* `lsblk`

#### Memory

* `free -h` → Shows total, used, free RAM and swap.
  
* `ps aux` → Shows memory usage (%MEM, RSS) per process.
  
* `top` → Shows per-process memory usage in real time.

#### CPU & Load

* `uptime` → Quick health check, shows the load averages for 1 minute, 5 minutes, 15 minutes.

* `vmstat`
  
* `top` & `ps aux` → Also shows the CPU Usage.
  
  * `wa` tag in top command shouws the I/O wait time.
  * `ni` tag shows indicates the priority of a process.Higher nice values mean lower priority.

#### Services and Systemd

* `systemctl` → systemctl is the control interface for systemd, the init system that starts, stops, manages boot order and handles logs(with journalctl)
  * `systemctl status ssh` → Check service status
  * `systemctl start nginx` → Start the service
  * `systemctl stop nginx` → Stop the service
  * `systemctl restart nginx` → Restart the service
  * `systemctl reload nginx` → Reload the service
  
* `journalctl` → Reads system logs from systemd.
  * `journalctl -xe`   {`-x` → Extra Expalantion, `-e` → Jump to recent logs}
  * `journalctl -u ssh -xe`
  * `journalctl --since "1 hour ago"`

* `resolvectl` → Controls DNS resolution
  * `sudo resolvectl dns ens5 8.8.8.8` → Sets the DNS for the interface.
  * `resolvectl status` → Shows which DNS servers are configured.
  * `sudo resolvectl revert ens5` → Revert back to the original DNS.

  
#### Files, Directories and Logs

* `ls` → Lists the files
  * `ls -l` → Long Format.
  * `ls -a` → Includes hidden files/folders like `.` and `..`
  * `ls -A` → Includes hidden files/folders except `.` and `..`
  * `ls -lh` → Human readable sizes.
  * **Output : -rw-r--r--  1 user group  1234 Jan 10 file.txt**
    * `-`	→ File Type {`-` → Regular File, `l` → Symbolic Link,`b` → Block Device(disk) , `s` → Socket, `d` → directory}
    * `rw-r--r--` →	permissions
    * `1`	→ link count
    * `user` →	owner
    * `group` → group
    * `1234` →	size (in bytes)
    * `Jan 10` →	mtime

* `.` → current directory
  
* `..` → parent directory

* `echo` → Prints text or variables to stdout. 
  * echo "hello" → Prints word "hello"
  * echo $HOME → Prints the value of HOME.
  * echo "log entry">>app.log → Redirects the "log entry" to app.log file.
 
* `printf` → Used to print the formatted output.
  * `printf "Hello World \n"` → {`\n` → Moves cursor to next line, `\t` → Spaces/tab, `\\` → Backslash }
  * ```
      name="Alice"
      age=25
      printf "Name: %s, Age: %d\n" "$name" "$age" 
    ```
    * Prints Name: Alice, Age: 25  {`%s` → `string`, `%d` → `integer`, `%f`	→ `float`}

* `pwd` → Print Working Directory              
  
* `cd` → Change Directory
    * `cd ~` → home directory
    * `cd ..` → parent directory
    * `cd -` → previous directory
    * `cd /` → root
    * cd /path || exit 1` → Try to change the directory and if it fails exit script with error.
      
* `stat file_name` → Provides all the informations like mtime, ctime, inode, timestamps and dilesystem details of the file_name.
  * `mtime` → Content Modification Time.
  * `ctime` → Metadata changed Time, including permissions, ownership, and also content changes.
  * `atime` → Last Access Time.
  * `ctime` → cannot be modified manually where as `atime` and `mtime` can be modified using touch commands.

* `file` → Detects file type based on content, not extension.
  * `file file_name`
  
* `cat` → non-interactive, prints entire file.
  * `cat file_name` → Shows the contents of the file. 
  * `cat>file_name` → Creates the file and opens editor and writes content to the file.
  * `cat>>file_name` → Append content to the file.
  
* `less` → Loads the file page by page and navigation is better.
  * `load file_name`  
    * `/pattern` → To search any pattern/word.
    * `n` → Next Match
    * `N` → Pervious Match
    * `G` → End of the file
    * `g` → Start of the file
    * `q` → Quit

* `head` → Shows the starting lines of the file.
  * `head file.txt` → Dispalys the firsy 10 lines of the file.
  * `head -n 20 file.txt`  → Dispalys the first 50 lines of the file.
   
* `tail` → To view last set of lines
  * `tail file.txt` → Dispalys the last 10 lines of the file.
  * `tail -n 50 file.txt` → Dispalys the last 50 lines of the file.
  * `tail -f app.log` → Used to view the live logs.

* `vim` → interactive editor, Ideal just for editing files.
  * `i` → insert mode.
  * `:wq` → write and quit.
  * `q!` → quit.
  * `gg` → Go to top of the file.
  * `G` → Go to bottom of the page.
  * `:4` or `:"4gg` → Got to line 4.
  * `yy` → Copy current line.
  * `3yy` → Copy the 3 lines from cursor.
  * `p` → Paste the content below cursor.
  * `3p` → Pastes the content 3 times.
  * `u` → Undo
  * `R` or `ctrl+r` → Redo
  * `/pattern` → Highlights matching patterns
  * `n` → Shows next match
  * `N` → Shows previous match
  * `Esc` → exits the search mode
  * `:34` → Shows line number 34
  
* `grep` → Searches the patterns in text
  * `-i` → `grep -i "error" file_name` → Ignore Case and search
  * `-n` → `grep -n "error" file_name` → Show Line Numbers
  * `-c` → `grep -c "error" file_name` → Count of matching pattern
  * `-r` → `grep -r "error" folder_path` → recursive search in folder
  * `-R` → `grep -R "error" folder_path` → follows symlink 
    
* `find` → Searches the filesystem in real time.
  * `-name` → `find /var/log -name "*.log"`
  * `-type` → `find /etc -type f` {type can be `f` → `File`, `d` → `Directory`, `l` → `Symbolic Link`}
  * `-iname` → `find . -iname "readme*"` → Ignore case of name.
  * `-mtime` → `-mtime -1` {Modified in last 1 day}
  * `-size` → `find / -type f -size +100M` {Files larger than 100MB}
  * `-exec` → `find . -type f -exec ls -lh {} \;`
    * `\;`
      * Runs command once per file.
      * Safer during changes and deletion commands.
    * `+`
      * Batch executes the files.
      * Faster execution. 
 
* `locate` → Searches for the files.
  * Searches in a cached database and is much faster but can be outdated.
  * `locate filename`

* `rm`
  * `-i` → Keeps the deletion process interactive. Rechecks before deleting.
  * `-r` → Recursive deletion, Used for deletion of files in folders.
  * `-f` → Force Deletion, No prompts are given.

* `ln` → Used to create links between files
  * `ln target_file symlink_name` 
    
#### File Permissions

* `chmod` → To change the permissions to owner, group, others.
  
    * `chmod g+w` → Add write permissions to groups.
    * `chmod u-x` → Removes execute permissions to user(owner).
    * Notations for providing permissions.
      * `read` → `4`
      * `write` → `2`
      * `execute` → `1`
        
* `chown` → To change the ownership of a file/directory.
  
  * `chown user_name:group_name file_name`   

### Netwroking

* `ip a` → Shows all the network interfaces & IPs.
  
* `ip route`
   
  * This shows where the packets are sent.
  * The most specific route wins, local subnets bypass gateways, and the default route forwards unknown traffic to the router.
  
* `hostname -I`
  
* `nslookup` → Queries DNS servers to resolve domain names to IP addresses(and vice versa).
  
  * `nslookup amazon.com`
  * `nslookup 8.8.8.8`
    
* `dig` → Powerful DNS query tool with detailed output.

  * `dig google.com`  
  * Records:
    * `A record` maps domain name to IPV4 Address
    * `AAAA record` maps domain name to IPV6 Address.
    * `CNAME` maps to alias to another domain.
    * `MX` maps to mail servers
    * `NS` maps to Name Servers     
  * Status :
    * `NOERROR` → Success
    * `NXDOMAIN` → Domain doesn’t exist
    * `SERVFAIL` → DNS server failure
    
* `host` → Lightweight DNS query tool.
  *  `host google.com`
  *  `host 8.8.8.8`
  
* `ping` → Used to check the reachability, network connectivity check and latency.   {**ICMP** is a network-layer protocol used for diagnostics and error reporting, not for application data.}
  * Sends the ICMP(Internet Control Message Protocol) Echo Requests. 
  * `ping google.com`
  * `ping -c 4 google.com`  {`-c` → Sends exactly 4 packets and stops}
  * `ping -c 4 8.8.8.8`
  
* `curl` → Transfers data using HTTP, HTTPS, FTP, etc.
  * `curl google.com`
  * `curl -I https://google.com` 
  
* `telnet` → Checks if a TCP port is reachable.
  * `telnet google.com 80`
  
* `nc` → Reads/writes data over TCP/UDP.
  * `nc -zv google.com 443` → Test port connectivity
  * `nc -l 8080` → Start a listener
  
* `ss -tuln` → Shows listening ports and connections.
  * `-t` → TCP
  * `-u` → UDP
  * `-l` → Listening
  * `-n` → Numeric

* `traceroute url`
  * `traceroute google.com`
  * It is a network diagnostic tool that maps the path packets take from your computer to a destination. 
  
* `netstat -tuln` → legacy version of `ss`

* `lsof -i :80` → To check which process is using port 80.
  
#### Default Ports 

* HTTP → 80
* HTTPS → 443
* SSH → 22
* DNS → 53
* FTP → 21
* MySQL → 3306
* Postgres → 5432

#### When something is “down/slow” on a Linux host:

* Is it up? → uptime / who
* CPU pressure? → top / vmstat 1
* Memory pressure? → free -h / look for swap, OOM
* Disk full / I/O? → df -h / iostat / dmesg
* Service running? → systemctl status <svc>
* Logs show why? → journalctl -u <svc> -n 200 --no-pager
* Is port open? → ss -lntp / curl -v localhost:<port>



