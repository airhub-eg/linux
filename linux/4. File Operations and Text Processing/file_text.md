# 4. File Operations and Text Processing

### 4.1 Adding Text to Files

**1. Using echo:**
```bash
echo "text" > file.txt       # Overwrite
echo "text" >> file.txt      # Append
```

**2. Using cat:**
```bash
cat > file.txt               # Type text, Ctrl+D to save
cat >> file.txt              # Append text, Ctrl+D to save
```

**3. Using printf:**
```bash
printf "text\n" >> file.txt
```

**4. Using Text Editors:**
```bash
nano file.txt
vi file.txt
```

### 4.2 Vi Editor

**Powerful text editor** in Linux/Unix systems (also known as Vim)

**Modes:**
1. **Command mode:** Default mode for navigation and commands
2. **Insert mode:** For inserting/modifying text (press `i`)
3. **Visual mode:** For selecting text blocks (press `v`)

**Opening and Saving:**
- Open: `vi filename`
- Save and exit: `Esc` then `:wq` or `Shift+ZZ`
- Discard and exit: `Esc` then `:q!`

**Navigation:**
- Arrow keys: Move cursor
- `0`: Beginning of line
- `$`: End of line
- `gg`: Beginning of file
- `G`: End of file

**Editing:**
- `x`: Delete character under cursor
- `dd`: Delete current line
- `u`: Undo last change
- `y`: Copy (yank) in visual mode
- `p`: Paste below cursor
- `P`: Paste above cursor

**Searching:**
- `/pattern` then Enter: Search forward
- `n`: Next occurrence
- `:%s/old/new/g`: Replace all occurrences

### 4.3 Input and Output Redirects

**1. Output Redirection (>):**
- Redirects output to file (overwrites)
```bash
echo "Hello, world!" > output.txt
```

**2. Output Redirection Appending (>>):**
- Appends output to file
```bash
echo "New line" >> output.txt
```

**3. Input Redirection (<):**
- Redirects file contents as input
```bash
sort < input.txt
```

### 4.4 Pipes

**Purpose:** Connect output of one command to input of another

**Syntax:**
```bash
command1 | command2
```

**Examples:**

1. **Filtering with grep:**
   ```bash
   ls -l | grep ".txt"
   ```

2. **Counting lines with wc:**
   ```bash
   cat file.txt | wc -l
   ```

3. **Sorting:**
   ```bash
   ls | sort
   ```

### 4.5 Tee Command

**Purpose:** Read from stdin, write to stdout AND files simultaneously

**Syntax:**
```bash
command | tee file.txt
```

**Examples:**

1. **Save output to file:**
   ```bash
   ls | tee output.txt
   ```

2. **Append to existing file:**
   ```bash
   echo "New content" | tee -a existing.txt
   ```

3. **Save to multiple files:**
   ```bash
   command | tee file1.txt file2.txt
   ```

### 4.6 File Maintenance Commands

**1. cp (Copy):**
```bash
cp source.txt destination.txt
cp -r source_dir destination_dir    # Recursive for directories
```

**2. rm (Remove):**
```bash
rm file.txt
rm -r directory                     # Recursive for directories
rm -f file.txt                      # Force removal
```

**3. mv (Move/Rename):**
```bash
mv old_name.txt new_name.txt        # Rename
mv file.txt /path/to/destination/   # Move
```

**4. rmdir (Remove Directory):**
```bash
rmdir empty_directory               # Only removes empty directories
```

### 4.7 File Display Commands

**1. cat:**
- Display entire file contents
```bash
cat file.txt
```

**2. less:**
- View file one page at a time (with scrolling/searching)
```bash
less file.txt
```
- Navigate: Space (next page), b (previous page), q (quit)

**3. more:**
- Similar to less, displays one screenful at a time
```bash
more file.txt
```

**4. head:**
- Display first few lines (default: 10)
```bash
head file.txt
head -n 20 file.txt                 # First 20 lines
```

**5. tail:**
- Display last few lines (default: 10)
```bash
tail file.txt
tail -n 20 file.txt                 # Last 20 lines
tail -f log file.txt                 # Follow file updates (useful for logs)
```

### 4.8 Text Processing Commands

**1. cut:**
Extract specific columns or fields

**Examples:**
```bash
cut -d ',' -f 1,3 filename.csv      # Extract columns 1 and 3 (comma-delimited)
cut -c 1-5 filename.txt             # Extract first 5 characters
cut -d ':' -f 2 filename.txt        # Extract field 2 (colon-delimited)
echo "Hello, World!" | cut -c 2-7   # Extract characters 2-7
```

**2. awk:**
Versatile text processing tool

**Examples:**
```bash
awk '{print $1, $3}' filename.txt                    # Print columns 1 and 3
awk '{sum += $1} END {print sum}' filename.txt       # Sum column 1
awk '$2 > 50' filename.txt                           # Filter rows where column 2 > 50
awk -F ',' '{print $1, $3}' filename.csv             # Use comma as separator
awk '$2 == "Open" {print} $2 != "Open" {print "Closed"}' file.txt
```

**3. grep:**
Search for patterns in files

**Examples:**
```bash
grep "apple" fruits.txt              # Search for "apple"
grep "^A" names.txt                  # Lines starting with "A"
grep -i "apple" fruits.txt           # Case-insensitive search
grep -v "apple" fruits.txt           # Inverted search (lines without "apple")
```

**4. egrep:**
Extended grep (supports extended regular expressions)

```bash
egrep "apple|banana" fruits.txt      # Lines containing "apple" OR "banana"
```

**5. uniq:**
Filter adjacent matching lines (show unique lines)

```bash
uniq filename.txt                    # Remove duplicate adjacent lines
uniq -c filename.txt                 # Count occurrences
```

**6. sort:**
Sort lines of text

```bash
sort filename.txt                    # Ascending alphabetical order
sort -r filename.txt                 # Descending order
sort -n numbers.txt                  # Numerical sort
sort filename.txt | uniq             # Sort and remove duplicates
sort filename.txt | uniq -d          # Show only duplicate lines
```

**7. wc (Word Count):**
Count lines, words, characters

```bash
wc filename.txt                      # Lines, words, characters
wc -l filename.txt                   # Count lines only
wc -w filename.txt                   # Count words only
wc -c filename.txt                   # Count characters only
wc -m filename.txt                   # Count bytes
wc file1.txt file2.txt               # Count multiple files
cat file.txt | wc -l                 # Count from stdin
```

**8. sed (Stream Editor):**
Text processing tool for search/replace, insertion, deletion

**Examples:**
```bash
sed 's/pattern/replacement/' filename.txt              # Replace first occurrence per line
sed 's/pattern/replacement/g' filename.txt             # Replace all occurrences
sed -i 's/pattern/replacement/g' filename.txt          # In-place editing
sed '/pattern/d' filename.txt                          # Delete lines matching pattern
sed '/pattern/i\inserted text' filename.txt            # Insert text before pattern
sed -n '5,10p' filename.txt                            # Print lines 5-10
sed -e 's/old1/new1/g' -e 's/old2/new2/g' file.txt    # Multiple commands
```

### 4.9 Compare Files

**1. cmp:**
Compare files byte by byte

```bash
cmp file1.txt file2.txt              # Shows first differing byte
cmp -s file1.txt file2.txt           # Silent mode (exit status only)
```

**2. diff:**
Compare files line by line

```bash
diff file1.txt file2.txt             # Show differences
diff -u file1.txt file2.txt          # Unified diff format (more context)
diff -q file1.txt file2.txt          # Quick check (only report if different)
diff -w file1.txt file2.txt          # Ignore whitespace differences
```

### 4.10 Compress and Uncompress Files

**Using tar and gzip:**

**Compress:**
```bash
tar -czf archive.tar.gz file1 file2 directory
```
- `-c`: Create archive
- `-z`: Use gzip compression
- `-f`: Specify filename

**Uncompress:**
```bash
tar -xzf archive.tar.gz
```
- `-x`: Extract
- `-z`: Use gzip decompression
- `-f`: Specify filename

**Using zip:**

**Compress:**
```bash
zip archive.zip file1 file2 directory
```

**Uncompress:**
```bash
unzip archive.zip
```
