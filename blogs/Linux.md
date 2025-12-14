# Level 0 — Terminal Foundations

**0.1 Shell + navigation**

* pwd/cd, absolute vs relative paths, `~ . ..`, `ls` vs `ls -la`, tab completion, history

**0.2 Files + permissions basics**

* file types (`- d l`), `chmod` numeric/symbolic, executable bit, shebang, `umask` intro

**0.3 Viewing files**

* `cat`, `less`, `head`, `tail`, `nl`, `wc`

**0.4 Searching + quoting + streams**

* `grep` flags, wildcards `* ? []`, quotes `' "` , stdout/stderr, `> >> 2> &>`

**0.5 Finding files**

* `find` basics, `locate/updatedb`, `xargs`, safe patterns (`-print0 | xargs -0`)

**0.6 Text processing pipelines**

* `sort`, `uniq`, `cut`, `paste`, `tr`, `tee`, `awk` intro, `sed` intro

**0.7 Editors**

* `nano` basics + survival `vim` (open/save/search/quit)

---

# Level 1 — Day-to-day Linux Power

**1.1 Archives + compression**

* `tar`, `gzip`, `bzip2`, `xz`, `zip/unzip`

**1.2 Packages**

* apt basics, repos, `dpkg`, installing/removing, troubleshooting deps

**1.3 Environment**

* env vars, PATH, `export`, `.bashrc`, aliases, functions

**1.4 Remote work**

* `ssh`, keys, `scp`, `rsync`, known_hosts, ssh config

**1.5 Networking basics**

* `ip a`, `ip r`, `ping`, `curl/wget`, DNS basics (`dig`), ports (`ss`)

---

# Level 2 — Users, Permissions, Processes

**2.1 Users & groups**

* `id`, `/etc/passwd`, `/etc/group`, `useradd/usermod`, `passwd`

**2.2 Sudo + privilege**

* sudoers, least privilege, `visudo`

**2.3 Permissions deep**

* special bits: setuid/setgid/sticky, default perms, `umask`, ACLs (`getfacl/setfacl`)

**2.4 Processes & jobs**

* `ps`, `top/htop`, job control `& fg bg jobs`, priorities `nice/renice`

**2.5 Signals**

* `kill`, signal types, graceful vs force, traps in bash

**2.6 Resource limits**

* `ulimit`, open files, core dumps basics

---

# Level 3 — Storage & Filesystems

**3.1 Disks & partitions**

* `lsblk`, `blkid`, `fdisk/parted` (concepts), GPT vs MBR

**3.2 Filesystems**

* ext4/xfs basics, `mkfs`, labels/UUIDs

**3.3 Mounting**

* `mount/umount`, `/etc/fstab`, persistent mounts

**3.4 Space & inodes**

* `df -h`, `du -sh`, inode exhaustion `df -i`

**3.5 Links**

* hard vs symlink, link count meaning, inode view `ls -li`

**3.6 Permissions + storage edge cases**

* “noexec”, “nosuid”, mount options, tmpfs

---

# Level 4 — System Administration Core

**4.1 Boot & startup**

* boot flow basics, GRUB concept, kernel/initramfs concept

**4.2 systemd services**

* units, `systemctl start/stop/status/enable`, service files

**4.3 Logging**

* `journalctl` filters, log locations, rotate basics

**4.4 Scheduling**

* `cron`, `at`, systemd timers

**4.5 Time**

* `date`, `timedatectl`, NTP concepts

**4.6 Software build basics**

* `make`, gcc basics, shared libs intro (`ldd`)

---

# Level 5 — Networking (Ops/Interview Heavy)

**5.1 Interfaces & routing**

* iproute2, routes, gateways, metrics

**5.2 DNS deep**

* resolv.conf/systemd-resolved, `dig`, troubleshooting

**5.3 Ports & connections**

* `ss -lntp`, `lsof -i`, NAT concept, ephemeral ports

**5.4 Packet capture**

* `tcpdump` basics, filters, reading symptoms

**5.5 Firewall basics**

* `ufw` / `iptables/nft` concepts, allow/deny

---

# Level 6 — Security Essentials

**6.1 SSH hardening**

* key-only auth, disable root login, sshd_config basics

**6.2 File integrity + permissions hygiene**

* secure defaults, secrets handling, least privilege

**6.3 Updates & vuln hygiene**

* unattended upgrades concept, patching workflow

**6.4 Auditing basics**

* logs, auth logs, `last`, `who`, `w`

---

# Level 7 — Bash & Automation

**7.1 Bash scripting fundamentals**

* variables, quoting, conditions, loops

**7.2 Functions + args**

* `$1..`, `$@`, exit codes `$?`, `getopts`

**7.3 Robust scripts**

* `set -euo pipefail`, traps, temp files, logging

**7.4 Text parsing in scripts**

* awk/sed/grep pipelines, config parsing patterns

**7.5 Mini projects**

* log analyzer, backup script, healthcheck script, deploy helper

---

# Level 8 — Troubleshooting & Performance

**8.1 Process debugging**

* `strace` basics, `lsof`, `/proc` overview

**8.2 CPU/memory**

* `top`, `free`, `vmstat`, load avg, OOM basics

**8.3 Disk**

* `iostat` (if available), `iotop` concept, `dmesg` clues

**8.4 Network troubleshooting**

* latency vs throughput, DNS vs routing, tcpdump evidence

**8.5 System bottleneck method**

* a repeatable checklist for incidents

---

# Level 9 — Advanced Linux Concepts

**9.1 Kernel/user space concepts**

* syscalls, kernel modules overview, `lsmod/modprobe`

**9.2 Namespaces & cgroups**

* containers foundations, isolation primitives

**9.3 Filesystem internals**

* page cache, buffer cache, fs journaling concept

**9.4 SELinux/AppArmor (concept-first)**

* modes, policies, debugging basics

---

# Level 10 — Interview Mastery Track

**10.1 Linux interview Q bank**

* commands, concepts, scenarios

**10.2 Practical labs**

* “broken DNS”, “disk full”, “service won’t start”, “high load”, “permission denied”

**10.3 Mock interview rounds**

* rapid-fire + deep-dive debugging + system design for ops





## Shell

A **shell** is the program (command interpretor) that reads your commands and runs them (for example, `bash` or `zsh`).

* `echo $SHELL` → Checks the default shell
* #!/bin/bash
    * Shebang
    * Required for executable scripts to indicate that the script needs to be executed using /bin/bash to Linux.

### Commands

* `echo` → Prints
* `whoami`
* `mkdir` → Make Directory
* `touch`
* `cat`
* `pwd`  
* `cd`→ Change Directory
* `stat file_name` → Gives all the information regarding the file_name.
* `ls` → Lists the files/folders.
* `chmod` → Change Permissions   
* `apropos` - Searches the system’s man-page database.
* `./file_name.sh`
* `bash file_name.sh`
* tail
* head
* less
* `|` 
* `seq`
* `stdout`
* `stderr`
* `grep`
* `find`
* `find . -type f -name "*.txt" -exec stat {} \;`
* `find . -type f -name "*.txt" -exec ls -l {} \;`
* `setgid`
* `rm`
* `xargs`
* `sort`
* `cut`
* `uniq`
* `awk`
* `sed`
* 


## Special Symbols 

* `.`  → current directory
* `..` → parent directory (one level up)
* `~`  → your home directory (IMPORTANT: it is `~`, not `!`)
* `-` → switches to the previous dierctory you are in and prints the directory.
* `$` →  value of the variable
* `>` → Output Direction
* `<<` → Here Document
* `2>`
* `&>`
* `''` nothing expands (literal text)
* `""` variables expand: $HOME, $name
* $(date)
