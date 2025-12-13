## Shell

A **shell** is the program (command interpretor) that reads your commands and runs them (for example, `bash` or `zsh`).

* `echo $SHELL` → Checks the default shell

### Commands

* `echo` → Prints
  
  * `echo $SHELL` 
  * `echo "hello"` > file_name → `>` overwrite
  * `echo "hello"` >> file_name → `>>` append
    
* `pwd`
  
* `cd`→ Change Directory
  
  * `cd .` → stays where you are
  * `cd ..` → goes up one folder
  * `cd ~` → goes to your home folder
  * `cd /` → go to root directory
  * `cd -` → go to the previous directory (toggle back)
  * `cd /etc` → go to /etc
    
* `ls` → Lists the files/folders.
  
  * `ls -lsa`
    * `-l` → long format
    * `-a` → all files (including hidden files that start with `.`)
    * `-s` → Shows disk space
    * `-h` → human sizes (K/M/G)
    * `-t` = sort by time (newest first)

**Output:** 
    -rw-r--r--  1 manideep manideep   3771 Dec 12 21:10 notes.txt
  * 1st char = **type**
    * `-` regular file
    * `d` directory
    * `l` symlink
    * `c` char device
    * `b` block device
    * `p` pipe
    * `s` socket  
  * Next 9 chars = **Permissions in 3 groups:**
    * owner: `rw-`
    * group: `r--`
    * others: `r--`   
  * **Link count**
    * For files: usually 1
    * For directories: often 2+ (because of `.` and `..`)
    * For hard links: will be >1  
  * **Owner (user)**
  * **Group**
  * **Size (bytes)**
  * **Modified time (mtime)**
  * **Name (and symlink target)**
          
* `chmod` → Change Permissions
  
  * `chmod 644 file_name` - Provides read and write to owner and read only to group and others.
  * `chmod u+x file_name` - Add execute permissions to user.
  * `chmod go-w file_name` - Remove write permissions to group and others.
    * `r` → 4
    * `w` → 2
    * `x` → 1
* `apropos` - Searches the system’s man-page database.
  * `apropos network` - searches for the entries with name or description matching 'network'.
* `sudo mandb` - Updates the mandb
* 
  

  



## Special Symbols 

* `.`  → current directory
* `..` → parent directory (one level up)
* `~`  → your home directory (IMPORTANT: it is `~`, not `!`)
* `$` →  value of the variable
  


