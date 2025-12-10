# 7. Networking

### 7.1 Network Configuration

**Enable Internet in VirtualBox:**
1. Go to Network settings in VirtualBox
2. Change adapter to "Bridged Adapter"
3. Select appropriate connection (wired or wireless)

### 7.2 ifconfig Command

**Purpose:** Display/configure network interfaces (part of net-tools package)

**View active interfaces:**
```bash
ifconfig
```

**Common Interfaces:**
- **enp1s0:** Ethernet card
- **lo:** Loopback interface
- **wlp2s0:** Wireless card

**Output Information:**
- UP: Interface is working
- Broadcasting and multicast support
- MTU (Maximum Transmission Unit): 1500 bytes (max packet size)
- inet: IPv4 address
- inet6: IPv6 address

**View specific interface:**
```bash
ifconfig enp1s0
```

**Enable/Disable Interface:**
```bash
ifconfig enp1s0 up                   # Enable
ifconfig enp1s0 down                 # Disable
```

**Options:**
- `-a`: View all interfaces (including inactive)
- `-s`: Short list of interfaces

### 7.3 ping Command

**Purpose:** Send echo requests to network hosts (check connectivity)

**Basic usage:**
```bash
ping google.com
```

**Limit packets:**
```bash
ping -c 5 google.com                 # Send 5 packets
```

**Use Cases:**
- Check internet connection
- Verify server availability
- Test network latency

### 7.4 route Command

**Purpose:** View and manipulate routing table

**View routing table:**
```bash
route
route -n                             # Numeric format
```

**Flag G:** Indicates default gateway

**Modify gateway:**
```bash
route del default                    # Delete default gateway
route add default gw 192.168.1.1     # Add new gateway
```

### 7.5 netstat Command

**Purpose:** Display network-related information

- Network connections
- Routing tables
- Interface statistics
- Protocol statistics

**Common Usage:**
```bash
netstat -tuln                        # TCP/UDP listening ports
netstat -r                           # Routing table
netstat -i                           # Interface statistics
```

**Port Information:**
List of well-known ports: `/etc/services`

### 7.6 Other Network Commands

**tcpdump:**
- Scans network interfaces
- Captures packet activity
- Parses and outputs packet information

**ethtool:**
- Query and control NIC settings
- Detailed interface information
- Change settings (speed, duplex mode, etc.)

### 7.7 NetworkManager

**Purpose:** Software utility for managing network connectivity on Linux

**Management Tools:**

**1. nmcli (NetworkManager CLI):**
- Command-line interface
- Useful when GUI unavailable
- Can be used in scripts

**2. nmtui (NetworkManager TUI):**
- Text user interface
- Runs in terminal window
- Menu-based selections

**3. nm-connection-editor:**
- Full graphical management tool
- Access most NetworkManager options
- Desktop/console access only

**4. GNOME Settings:**
- Network screen in GNOME desktop
- Basic network management tasks

### 7.8 wget Command

**Purpose:** Non-interactive download of files from web

**Features:**
- Supports HTTP, HTTPS, FTP
- Supports HTTP proxy retrieval

**Example:**
```bash
wget www.google.com                  # Downloads homepage HTML
wget -O filename.html www.google.com # Save with specific name
wget -c url                          # Continue interrupted download
```

### 7.9 curl Command

**Purpose:** Transfer data from/to server

**Supported Protocols:**
- HTTP, HTTPS, FTP, SMTP, and more

**Usage:**

**Check page availability:**
```bash
curl www.google.com                  # Display content
```

**Save output:**
```bash
curl -o filename.html www.google.com
```

**Download file:**
```bash
curl -O http://example.com/file.zip  # Save with original name
```

**Other Options:**
- `-I`: Fetch headers only
- `-L`: Follow redirects
- `-u user:pass`: Authentication

### 7.10 FTP (File Transfer Protocol)

**Purpose:** Transfer files between client and server

**Port:** 21 (default)

**Server Setup:**

1. **Install FTP daemon:**
   ```bash
   sudo apt install vsftpd
   ```

2. **Configure:**
   Edit `/etc/vsftpd.conf`:
   - Uncomment required lines
   - Add: `write_enable=YES`
   - Add: `local_umask=022`

3. **Start service:**
   ```bash
   sudo systemctl start vsftpd
   sudo systemctl enable vsftpd       # Enable at boot
   ```

**Client Setup:**

1. **Install FTP client:**
   ```bash
   sudo apt install ftp
   ```

2. **Get server IP:**
   ```bash
   ifconfig                           # On server
   ```

3. **Connect:**
   ```bash
   ftp 192.168.1.10                   # Server IP
   ```
   - Enter username and password

**FTP Commands:**
- `bi`: Binary mode
- `hash`: Progress bar
- `put filename`: Upload file
- `get filename`: Download file
- `pwd`: Print working directory
- `cd`: Change directory
- `cdup`: Parent directory
- `mkdir/mkd`: Create directory
- `ls`: List files
- `bye/quit`: Exit

### 7.11 SSH (Secure Shell)

**Purpose:** Cryptographic network protocol for secure communication

**Features:**
- Secure remote command-line access
- Encrypted file transfer
- Authentication via cryptographic keys
- Session key encryption

**Port:** 22 (default)

**Server Setup:**

1. **Install SSH server:**
   ```bash
   sudo apt install openssh-server
   ```

2. **Start and enable:**
   ```bash
   sudo systemctl start sshd
   sudo systemctl enable sshd
   sudo systemctl status sshd         # Check status
   ```

**Client Connection:**

1. **Get server IP:**
   ```bash
   ifconfig                           # On server
   ```

2. **Connect:**
   ```bash
   ssh username@192.168.1.10          # Server IP
   ```
   - Enter password
   - Full terminal access to server

### 7.12 SCP (Secure Copy Protocol)

**Purpose:** Secure file transfer based on SSH

**Port:** 22 (uses SSH)

**Features:**
- Encrypted file transfers
- Works between local and remote hosts
- Between two remote hosts

**Prerequisites:**
- SSHD service enabled on server
- SCP package on client

**Upload File to Server:**
```bash
scp localfile.txt username@192.168.1.10:/remote/directory/
```

**Download File from Server:**
```bash
scp username@192.168.1.10:/remote/file.txt /local/directory/
```

**Copy Directory (recursive):**
```bash
scp -r localdirectory username@192.168.1.10:/remote/path/
```

**Between Two Remote Hosts:**
```bash
scp user1@host1:/file.txt user2@host2:/destination/
```

### 7.13 rsync Command

**Purpose:** Efficiently synchronize files/directories

**Key Features:**
- **Delta-transfer algorithm:** Transfers only differences
- Reduces data transmission
- Faster for large files with small changes
- Supports local and remote transfers
- Directory synchronization (identical file structures)

**Basic Syntax:**
```bash
rsync [OPTIONS] source destination
```

**Common Options:**
- `-a`: Archive mode (preserves links, permissions, ownership, etc.)
- `-z`: Compression
- `-v`: Verbose (display transferred files)
- `-r`: Recursive
- `--progress`: Show progress

**Examples:**

**1. Local synchronization:**
```bash
rsync -avz source/ destination/
```

**2. Synchronize file:**
```bash
rsync -avz file.txt destination/
```

**3. Remote transfer (upload):**
```bash
rsync -avz localdir/ username@192.168.1.10:/remote/directory/
```

**4. Remote transfer (download):**
```bash
rsync -avz username@192.168.1.10:/remote/directory/ localdir/
```

**5. Append to existing file:**
```bash
echo "New content" | rsync -av - username@host:/path/file.txt
```

**6. Multiple files to remote:**
```bash
rsync -avz file1.txt file2.txt username@host:/destination/
```

**Advantages:**
- Only changed portions transmitted
- Preserves file attributes
- Can resume interrupted transfers
- Bandwidth-efficient
