# 2. File System Structure and Navigation

### 2.1 What is a File System?

A **file system** is:
- A system used by OS to manage files and directories
- Controls how data is saved/retrieved from hard disk
- Stores files and directories in an organized, structured way

**Examples:**
- System configuration files → specific folder
- User files → another folder
- Log files → separate folder
- Commands/scripts → different folder

**File System Types:**
- **Linux:** ext3, ext4, xfs
- **Windows:** NTFS, FAT

### 2.2 File System Structure

**Key Directories:**

1. **/boot:**
   - Contains boot loader files
   - Grub documentation, configuration files
   - First location checked during system boot

2. **/root:**
   - Root user's home directory
   - Not to be confused with "/" (root directory)

3. **/dev:**
   - System devices (discs, CD-ROM, speakers, flash drives, keyboards)
   - Peripheral devices appear as files here

4. **/etc:**
   - All configuration files
   - Configuration for applications like sendmail, NFS, NTP
   - Applications running on top of Linux system

5. **/bin or /usr/bin:**
   - Essential binary files and commands
   - Everyday user commands (ls, pwd, etc.)

6. **/sbin or /usr/sbin:**
   - System administration binaries/commands
   - Commands for system-level purposes

7. **/opt:**
   - Optional add-on applications
   - Third-party applications (Oracle, SAP)
   - Not OS-bundled applications

8. **/proc:**
   - Files for all running processes
   - **Important:** Empty when system is shut down
   - Dynamic directory

9. **/lib:**
   - Libraries required by system and applications
   - C programming library files
   - Needed for commands and applications (written in C/C++)

10. **/tmp:**
    - Temporary files

11. **/home:**
    - Home directories for individual users

12. **/var:**
    - Variable data: logs, cache files, spool directories

13. **/mnt:**
    - Mount external file systems
    - **Mounting:** Process of attaching storage devices to file system at specific directory

14. **/media:**
    - CD-ROM mounting location
    - Used when CD-ROM drive has media inserted

### 2.3 Types of Users

**1. Regular User:**
- Created during Ubuntu installation
- Files/folders stored in /home directory
- No access to other users' directories
- Limited privileges

**2. Root User:**
- Known as superuser or administrator
- Created at installation time
- Highest level of privileges and permissions
- Unrestricted access to all files, directories, and system resources
- Can perform any action:
  - Modify system files
  - Install software
  - Change system configurations
  - Manage other user accounts

### 2.4 Difference Between "/" and "/root"

**1. "/" (Root Directory):**
- Top-level directory in file system hierarchy
- Starting point for entire directory structure
- All other directories located within (directly or indirectly)
- Represented by forward slash "/"
- Absolute path notation
- Contains system directories: /bin, /etc, /home, /var, /usr, etc.

**2. "/root" (Root User's Home Directory):**
- Home directory specifically for root user
- Unlike regular users (home under /home), root user's home is at /root
- Administrative user's personal directory

### 2.5 Linux Commands Basics

**Command Syntax:**
- Commands are **case-sensitive**
- Options may be letters or words

**Three formats:**
1. Command without option: `command [input] [output]`
2. Command with letter option: `command -letter [input] [output]`
3. Command with word option: `command --word [input] [output]`

### 2.6 File System Navigation Commands

**1. cd (Change Directory):**
- Changes directory using relative or absolute path
- Examples:
  - `cd /home/user/Documents` (absolute path)
  - `cd Documents` (relative path)
  - `cd ..` (parent directory)
  - `cd ~` (home directory)

**2. pwd (Print Working Directory):**
- Displays current directory location
- Example: `pwd` → `/home/user/Documents`

**3. ls (List):**
- Lists contents of directory
- Options:
  - `ls -l` (long format with details)
  - `ls -a` (include hidden files)
  - `ls -lh` (human-readable sizes)

### 2.7 Linux File Properties

**Command:** `ls -l`

**Output format:**
```
Type | Permissions | Links | Owner | Group | Size | Month | Day | Time | Name
-    | rw-r--r--   | 1     | omar  | omar  | 11   | Dec   | 3   | 2025 | test.txt
```

### 2.8 Linux File Types

| Symbol | Meaning |
|--------|---------|
| - | Regular file |
| d | Directory |
| l | Link (symbolic link) |
| c | Character device file |
| s | Socket |
| p | Pipe |
| b | Block device |

### 2.9 File System Paths

**1. Absolute Path:**
- Always begins with "/" (slash)
- Starts at root directory
- Example: `/home/user/Documents/file.txt`

**2. Relative Path:**
- Identifies location relative to current position
- No leading slash
- Example: `Documents/file.txt` (from /home/user)

### 2.10 Creating Files and Directories

**Creating Directories (mkdir):**

1. **Single directory:**
   ```bash
   mkdir Documents
   ```

2. **Multiple directories:**
   ```bash
   mkdir Pictures Music Videos
   ```

3. **Create with parent directories:**
   ```bash
   mkdir -p /home/user/Documents
   ```

4. **Nested directories:**
   ```bash
   mkdir Documents/Projects
   ```

5. **Multiple nested directories:**
   ```bash
   mkdir -p Documents/Work/Reports
   ```

**Creating Files:**

1. **Empty file (touch):**
   ```bash
   touch myfile.txt
   ```

2. **With text editor:**
   ```bash
   nano myfile.txt
   ```

3. **With output redirection:**
   ```bash
   echo "Hello, World!" > myfile.txt
   ```

### 2.11 Finding Files and Directories

**find Command:**
- Searches based on various criteria (name, size, type, modification time)
- Traverses directory hierarchy from given path
- Real-time search (examines file system at execution time)
- Powerful but slower for large directory structures

**Examples:**
1. **Find by name:**
   ```bash
   find /home/user -name "example.txt"
   ```

2. **Find directories:**
   ```bash
   find /var/www -type d
   ```

**locate Command:**
- Uses pre-built database (locate database)
- Database updated periodically (usually daily) by cron job
- Faster than find
- May not provide real-time results if database outdated
- Matches search pattern anywhere in file path

**Examples:**
```bash
locate example.txt
```

**Important:**
- Before using locate, run: `updatedb`
- May need root access: `sudo su`

**Key Difference:**
- **find:** Real-time search, complex criteria, slower
- **locate:** Database search, faster, may be outdated

### 2.12 Wildcards

Wildcards represent patterns to match multiple filenames.

**1. Asterisk (*):**
- Matches any sequence of characters (including none)
- Examples:
  - `ls *.txt` - all .txt files
  - `cp file* destination/` - all files starting with "file"

**2. Question Mark (?):**
- Matches any single character
- Examples:
  - `ls file?.txt` - matches file1.txt, fileA.txt (not file10.txt)
  - `rm ?.txt` - removes single-character filename with .txt

**3. Brackets ([ ]):**
- Specifies range or set of characters
- Examples:
  - `ls file[123].txt` - matches file1.txt, file2.txt, file3.txt
  - `rm file[!12].txt` - removes file3.txt, file4.txt (keeps file1.txt, file2.txt)

**4. Brace Expansion ({ }):**
- Generates multiple strings based on pattern
- Examples:
  - `mv file{1,2,3}.txt destination/`
  - `echo {apple,banana}_{red,green}` → apple_red, apple_green, banana_red, banana_green

**5. Character Classes:**
- Specifies range or set of characters for single character match
- Examples:
  - `ls file[0-9].txt` - file1.txt through file9.txt
  - `ls file[[:alpha:]].txt` - fileA.txt, fileB.txt (not file1.txt)

**6. Negation:**
- Excludes certain characters/patterns
- Examples:
  - `ls file[!1-9].txt` - fileA.txt, fileB.txt (not file1-9.txt)
  - `ls file[![:digit:]].txt` - excludes digit filenames

### 2.13 Soft Links and Hard Links

**Inode:**
- Pointer or number assigned to file on hard disk
- Computer understands numbers, not names
- Every file gets unique inode number
- Used to retrieve/read file data

**1. Soft Link (Symbolic Link/Symlink):**
- Special file type pointing to another file/directory by name
- Can span different file systems/partitions
- Functions as shortcut or alias
- Breaks if target file moved/deleted
- Can point to directories, files, or non-existing locations

**Creating soft link:**
```bash
ln -s target.txt link
```

**2. Hard Link:**
- Direct reference to physical data of file/directory
- Can only be created for files (not directories)
- Shares same inode as original file
- Still accesses data if original moved/deleted
- Cannot point to non-existing locations

**Creating hard link:**
```bash
ln target.txt link
```

**Usage Summary:**
- **Soft links:** Shortcuts, referencing files in different locations
- **Hard links:** Additional references to same physical data
