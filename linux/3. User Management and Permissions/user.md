# 3. User Management and Permissions

### 3.1 File Permissions

**Purpose:** Control access to files and directories

**Permission Types:**
- **r (read):** View file contents or list directory
- **w (write):** Modify file or directory contents
- **x (execute):** Run file as program or access directory

**Three Permission Sets:**
1. **User (owner)** permissions
2. **Group** permissions
3. **Other (everyone else)** permissions

### 3.2 Character Representation

**Symbols:**
- r = read
- w = write
- x = execute
- \- = no permission

**Permission Groups:**
- **u** = User (owner)
- **g** = Group
- **o** = Other
- **a** = All (user, group, other)

**Granting/Revoking:**
- **+** = Add permission
- **-** = Remove permission
- **=** = Set exact permission

**Examples:**
```bash
chmod u+x file.txt        # Add execute for user
chmod g-w file.txt        # Remove write for group
chmod o+r file.txt        # Add read for others
chmod a+x script.sh       # Add execute for all
chmod u=rwx,g=rx,o=r file.txt  # Set specific permissions
```

### 3.3 Numeric Representation

**Permission Values:**
- **Read (r):** 4
- **Write (w):** 2
- **Execute (x):** 1
- **No permission (-):** 0

**Calculate by summing values:**
- rwx = 4+2+1 = 7
- rw- = 4+2+0 = 6
- r-x = 4+0+1 = 5
- r-- = 4+0+0 = 4

**Common Permission Codes:**
- **644:** rw-r--r-- (owner read/write, group/others read)
- **755:** rwxr-xr-x (owner all, group/others read/execute)
- **777:** rwxrwxrwx (all permissions for everyone)
- **700:** rwx------ (owner all, no access for others)

**Examples:**
```bash
chmod 644 filename.txt
chmod 755 script.sh
chmod 600 private.txt
```

### 3.4 File and Directory Ownership

**Ownership Information:**
- Each file/directory has an **owner** and a **group**
- Stored as User IDs (UIDs) and Group IDs (GIDs)

**1. Checking Ownership:**
```bash
ls -l filename
```
Output format: `owner group`

**2. Changing Ownership (chown):**
```bash
chown new_owner filename
chown new_owner:new_group filename
chown :new_group filename          # Change group only
```

**3. Using UIDs and GIDs:**
```bash
chown 1001:1002 filename
```

**Important:** Changing ownership requires root/administrator privileges

### 3.5 Access Control Lists (ACL)

**Purpose:** More fine-grained access control than traditional permissions

**Advantages:**
- Set permissions for multiple users and groups
- Grant/deny specific permissions to each

**Viewing ACLs:**
```bash
getfacl filename
```

**Setting ACLs:**
```bash
setfacl -m u:username:rwx filename      # User ACL
setfacl -m g:groupname:rx filename      # Group ACL
setfacl -m u:username:rw directory      # Directory ACL
```

**Modifying ACLs:**
```bash
setfacl -m u:username:r filename
```

**Removing ACLs:**
```bash
setfacl -b filename                     # Remove all ACLs
setfacl -x u:username filename          # Remove specific user ACL
```
