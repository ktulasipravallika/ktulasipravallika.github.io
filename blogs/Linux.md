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
      * Communicates with hardware via device drivers
      * Abstracts hardware details from user programs
   * File System Management
      * Handles files, directories, permissions
      * Interfaces with filesystems like ext4, xfs
   * System Call Interface
      * Provides a secure interface between user space and kernel space.
      * Examples: read(), write(), open(), fork()

### Kernel Space vs User Space

Kernel space runs privileged code, user space runs applications, and system calls act as the controlled bridge between them.

#### **Kernel Space**
   * Where the **Linux kernel runs**
   * Has **full access** to hardware (CPU, memory, devices)
   * Executes **privileged instructions**
   * A bug here can **crash the entire system**
   * Examples: 
      * Process scheduler
      * Memory manager
      * Device drivers
      * Filesystem code

#### **User Space**

* Where **applications run**
* Has **restricted access**
* Cannot directly access hardware
* Must request services from kernel
* Examples:
   * Shell (`bash`)
   * Commands (`ls`, `ps`, `grep`)
   * Applications (databases, web servers)
   * Docker, Java, Python programs
* `ls` command runs in user space because it is a regular user program. When it needs information (like directory contents), it makes system calls to the kernel, which then accesses the filesystem and returns the results.

### System Call

* A system call is a controlled interface that allows a user-space program to request services from the kernel, such as accessing files, memory, processes, or devices.
* User programs cannot directly access hardware
* Kernel protects the system from unsafe operations
* System calls provide a safe boundary
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

**Note :**

* Execute on a directory → ability to enter it.
* Read on a directory → ability to list files.
  
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
      
      * **General flow** : Parent fork() →  child → Child exits → Parent calls wait() → Kernel removes child from process table → No zombie.
        
      * **Zombie process** : Parent fork() → child → Child exits → Parent never calls wait() → Zombie process remains.
        
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

     
## Commands

* `#!/bin/bash` → Shebang
* `echo` →
* `./file_name` →
* `df -h` → To check the disk usage per filesystem.          {`-h` → human readable format}
* `du -sh /*` → To check the disk usage of all the directories.

#### File Permissions

* `chmod` → To change the permissions to owner, group, others.
* `chown` → To change the ownership of a file/directory.
  
#### Users and Groups

*  `cat /etc/passwd` →
*  `cat /etc/group` →
*  `useradd user_name` →
*  `userdel user_name` →
*  `groupadd group-name` →
*  `groupadel group-name` →

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
