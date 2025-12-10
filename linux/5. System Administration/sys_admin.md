## 5. System Administration

### 5.1 User Account Management

**Adding Users:**

1. **Basic user creation:**
   ```bash
   useradd username
   ```

2. **With options:**
   ```bash
   useradd -m -s /bin/zsh username
   ```
   - `-m`: Create home directory
   - `-s`: Set default shell

3. **Set password:**
   ```bash
   passwd username
   ```

**Adding Groups:**

1. **Create group:**
   ```bash
   groupadd groupname
   ```

2. **With specific GID:**
   ```bash
   groupadd -g 1001 groupname
   ```

3. **Add user to group at creation:**
   ```bash
   useradd -G groupname username
   ```

**Deleting Users:**

1. **Delete user account:**
   ```bash
   userdel username
   ```

2. **Delete with home directory:**
   ```bash
   userdel -r username
   ```
   - `-r`: Remove home directory and mail spool

**Deleting Groups:**

1. **Delete group:**
   ```bash
   groupdel groupname
   ```

2. **Force delete:**
   ```bash
   groupdel -f groupname
   ```

**Important:** Deleting a user doesn't automatically delete their files/directories

### 5.2 Switch User

**Command:**
```bash
su - username
```
- Enter password when prompted
- Without username, switches to root by default

**Alternative:**
```bash
sudo -u username command             # Run specific command as another user
```

**Exit switched session:**
```bash
exit
# or
Ctrl+D
```

**Notes:**
- Inherits environment variables, permissions, shell of that user
- Requires administrative privileges (sudo or root access)

### 5.3 Monitor Users

**1. who command:**
Shows currently logged-in users

```bash
who
```

**Output:**
```
user1    tty1         2022-12-01 10:00
user2    pts/0        2022-12-01 11:30 (192.168.0.10)
```
- Username
- Terminal/device
- Login date & time
- Remote address (if applicable)

**2. last command:**
Shows previous login sessions

```bash
last
```

**Output:**
```
user1    pts/0    192.168.0.10    Thu Dec 1 10:00   still logged in
user2    pts/1    192.168.0.20    Thu Dec 1 11:30 - 12:00  (00:30)
```

**3. w command:**
Summary of logged-in users and activities

```bash
w
```

**Output columns:**
- **USER:** Username
- **TTY:** Terminal/device
- **FROM:** Remote IP/hostname
- **LOGIN@:** Login time
- **IDLE:** Idle time
- **JCPU:** Cumulative CPU time
- **PCPU:** Current process CPU time
- **WHAT:** Current command/process

**4. id command:**
Display user and group IDs

```bash
id                                   # Current user
id username                          # Specific user
```

**Output:**
```
uid=1000(user) gid=1000(user) groups=1000(user),4(adm),24(cdrom),27(sudo)
```

### 5.4 Talking to Users

**wall command:**
Send message to all logged-in users

**Usage:**
1. Type: `wall`
2. Enter message
3. Press `Ctrl+D` to send

**write command:**
Send message to specific user

**Usage:**
```bash
write username
```
Then type message and press Enter to send

### 5.5 System Utility Commands

**1. date:**
Display/set system date and time
```bash
date
```

**2. uptime:**
System uptime and load average

```bash
uptime
```

**Output:**
```
17:32:45 up 3 days, 2:15, 4 users, load average: 0.12, 0.18, 0.20
```
- Current time
- System uptime
- Number of logged-in users
- Load average (1, 5, 15 minutes)

**3. uname:**
Display system information

```bash
uname -a                             # All information
uname -s                             # Kernel name
uname -r                             # Kernel release
uname -m                             # Machine hardware name
```

**Output:**

```
Linux mymachine 4.15.0-54-generic #58-Ubuntu SMP Mon Jun 24 10:55:24 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```

**4. which:**
Locate executable file of command

```bash
which ls                             # Output: /bin/ls
which bash                           # Find shell location
```

**Note:** Built-in commands (like `cd`) won't show output

### 5.6 systemctl Command

**Purpose:** Manage systemd service manager

**Basic Operations:**

1. **Start service:**
   ```bash
   systemctl start service_name
   ```

2. **Stop service:**
   ```bash
   systemctl stop service_name
   ```

3. **Restart service:**
   ```bash
   systemctl restart service_name
   ```

4. **Enable at boot:**
   ```bash
   systemctl enable service_name
   ```

5. **Disable at boot:**
   ```bash
   systemctl disable service_name
   ```

6. **Check status:**
   ```bash
   systemctl status service_name
   ```

**Listing Units:**

```bash
systemctl list-units                 # All loaded units
systemctl list-units --state=active  # Active units only
systemctl list-units --state=inactive # Inactive units only
systemctl list-units --state=failed  # Failed units only
systemctl list-units --type=service  # Services only
systemctl list-units --all --no-pager # Short format
```

### 5.7 top Command

**Purpose:** Display real-time system resource usage

**Key Information Sections:**

**1. Header Information:**
- System uptime
- Number of logged-in users
- Load averages (1, 5, 15 minutes)

**2. CPU Usage:**
- CPU states (user, system, idle)
- CPU load averages

**3. Memory Usage:**
- Total memory
- Used memory
- Free memory
- Shared memory
- Buffers/cache

**4. Swap Usage:**
- Total swap
- Used swap
- Free swap

**5. Tasks:**
- Total processes
- Running processes
- Sleeping processes
- Zombie processes (completed but still in process table)

**6. Process Information:**
- **PID:** Process ID
- **USER:** User running process
- **PR:** Scheduling priority
- **NI:** Nice value (negative = higher priority, positive = lower priority)
- **VIRT:** Total virtual memory used
- **RES:** Shared memory (RAM consumption)
- **%CPU:** CPU usage percentage
- **%MEM:** Memory usage percentage
- **TIME+:** Total CPU time
- **COMMAND:** Program name

**Interactive keys:**
- `q`: Quit
- Various keys for sorting, changing display format, adjusting update interval

### 5.8 System Run Levels

**Purpose:** Predefined operating states determining which services start/stop

**Run Levels (SysVinit):**

- **0: Halt/Shutdown** - System halts, no services active
- **1: Single User Mode** - Minimal runlevel, one user, maintenance/recovery
- **2: Multi-User (no networking)** - Multi-user without network services
- **3: Multi-User (with networking)** - Full multi-user with networking, most services active
- **4: Undefined** - User-defined customization
- **5: GUI** - Graphical interface (X Window System)
- **6: Reboot** - System reboot

### 5.9 Computer Boot Process

**Step-by-step process:**

1. **Power Supply:**
   - Electricity provided to computer
   - Power flows through motherboard

2. **CPU Startup:**
   - CPU powers up first
   - Pulls instructions from BIOS

3. **BIOS (Basic Input/Output System):**
   - Software built by manufacturer
   - Installed on ROM chip on motherboard
   - Contains startup instructions

4. **CMOS (Complementary Metal-Oxide Semiconductor):**
   - Chip near BIOS on motherboard
   - Contains BIOS settings: system time, date, hardware settings
   - Powered by battery (not regular power)

5. **POST (Power-On Self-Test):**
   - BIOS instructs CPU to test all attached devices
   - Ensures devices are in working condition
   - Boot fails if test fails

6. **Disk Access:**
   - BIOS instructions direct to disk
   - Looks for first sector on disk

7. **MBR (Master Boot Record):**
   - First sector on disk
   - Contains OS information (Windows, Linux, etc.)

8. **OS Loading:**
   - OS loaded to RAM/memory
   - Has own set of instructions
   - Applications load
   - CPU processes instructions

