# 6. Shell Scripting

### 6.1 What is a Shell?

**Definition:**
- Interface between user and kernel
- Acts as command interpreter
- Translates terminal input into system actions

**History:**
- **Bourne shell (sh):** Created by Stephen Bourne in 1970s, widely used
- **Bourne-Again shell (bash):** Introduced 1989 by Brian Fox for GNU project
- **bash:** Default shell for many Unix-like systems including Linux

**Built-in Commands:**
Commands executed directly in shell without calling another program:
- cd, echo, eval, exec, exit, export, pwd, set, read, test, trap, etc.

### 6.2 Shell Scripting Basics

**What is Shell Scripting?**
- Text file containing series of commands
- Used for automating tasks
- Executes commands sequentially
- Like entering commands directly in CLI

**Features:**
- Supports variables, loops, conditional statements, functions
- Includes system commands, executable programs, built-in shell commands
- Useful for text processing (awk, sed, grep)
- Can call external programs (Python, Perl, Ruby)
- Generally portable across Unix-like systems

**Creating Shell Script:**

1. **Create file:**
   ```bash
   touch script.sh
   ```

2. **Make executable:**
   ```bash
   chmod a+x script.sh
   ```

3. **First line (shebang):**
   ```bash
   #!/bin/bash
   ```

4. **Comments:**
   ```bash
   # This is a single-line comment
   ```

**Running Script:**
```bash
./script.sh
```

### 6.3 Variables in Shell

**Basic Usage:**

**Define variable:**
```bash
variable_name=value
```

**Access variable:**
```bash
echo $variable_name
```

**Example:**
```bash
#!/bin/bash
name="John"
echo "Hello, $name"
```

**Read-only Variables:**
```bash
readonly variable_name=value
```
Content cannot be changed after declaration

### 6.4 Special Variables

- **$$:** Process number of current bash shell
- **$?:** Exit status of last command (0 = success, non-zero = error)
- **$#:** Number of input arguments
- **$* or $@:** All input arguments
- **$!:** Process number of last background process
- **$n:** Value of nth argument (n=1,2,3,...)

**Example:**
```bash
#!/bin/bash
echo "Script PID: $$"
echo "Number of arguments: $#"
echo "All arguments: $*"
echo "First argument: $1"
```

### 6.5 Reading User Input

**read command:**
```bash
#!/bin/bash
echo "Enter your name:"
read name
echo "Hello, $name"
```

**Multiple inputs:**
```bash
read first_name last_name
echo "Welcome $first_name $last_name"
```

### 6.6 Arithmetic Operations

**Syntax:**
```bash
result=$((expression))
```

**Operations:**
- Addition: +
- Subtraction: -
- Multiplication: *
- Division: /
- Exponentiation: **
- Modulus: %

**Example:**
```bash
#!/bin/bash
a=10
b=5
sum=$((a + b))
product=$((a * b))
echo "Sum: $sum"
echo "Product: $product"
```

### 6.7 Conditional Statements

**if-then-else Syntax:**
```bash
if [ condition ]
then
    # Commands if true
else
    # Commands if false
fi
```

**if-elif-else:**
```bash
if [ condition1 ]
then
    # Commands for condition1
elif [ condition2 ]
then
    # Commands for condition2
else
    # Commands if all false
fi
```

**Numeric Comparison Operators:**
- **-eq:** Equal to
- **-ne:** Not equal to
- **-gt:** Greater than
- **-lt:** Less than
- **-ge:** Greater than or equal to
- **-le:** Less than or equal to

**Example:**
```bash
#!/bin/bash
read -p "Enter a number: " num
if [ $num -gt 0 ]
then
    echo "Positive"
elif [ $num -lt 0 ]
then
    echo "Negative"
else
    echo "Zero"
fi
```

### 6.8 case-esac Statement

**Syntax:**
```bash
case $variable in
    pattern1)
        commands
        ;;
    pattern2)
        commands
        ;;
    *)
        # Default case
        commands
        ;;
esac
```

**Example:**
```bash
#!/bin/bash
read -p "Enter fruit name: " fruit
case $fruit in
    apple)
        echo "Color: Red"
        ;;
    banana)
        echo "Color: Yellow"
        ;;
    grape)
        echo "Color: Purple"
        ;;
    *)
        echo "Unknown fruit"
        ;;
esac
```

### 6.9 Loops

**while Loop:**
```bash
while [ condition ]
do
    commands
done
```

**Example:**
```bash
#!/bin/bash
counter=1
while [ $counter -le 5 ]
do
    echo "Count: $counter"
    counter=$((counter + 1))
done
```

**for Loop:**
```bash
for item in items
do
    commands
done
```

**Example:**
```bash
#!/bin/bash
for i in 1 2 3 4 5
do
    echo "Number: $i"
done

# Range syntax
for i in {1..10}
do
    echo $i
done

# C-style for loop
for ((i=1; i<=10; i++))
do
    echo $i
done
```

**Loop Control:**
- **break:** Exit loop
- **continue:** Skip current iteration
- **sleep n:** Delay n seconds

### 6.10 Arrays

**Declaration:**
```bash
array_name=(item1 item2 item3)
```

**Accessing Elements:**
```bash
echo ${array_name[0]}                # First element
echo ${array_name[*]}                # All elements
echo ${array_name[@]}                # All elements (alternative)
echo ${#array_name[@]}               # Array length
```

**Adding Elements:**
```bash
array_name[3]=item4
array_name+=(item5)                  # Append
```

**Example:**
```bash
#!/bin/bash
fruits=(apple banana cherry)
echo "First fruit: ${fruits[0]}"
echo "All fruits: ${fruits[*]}"
fruits[3]=orange
echo "Updated: ${fruits[*]}"
```

### 6.11 Functions

**Syntax:**
```bash
function_name() {
    commands
}
```

**Calling Function:**
```bash
function_name
```

**Example:**
```bash
#!/bin/bash
greet() {
    echo "Hello, World!"
}

greet
```

**Passing Arguments:**
```bash
function_name() {
    echo "Argument 1: $1"
    echo "Argument 2: $2"
}

function_name arg1 arg2
```

**Return Values:**
```bash
calculate_sum() {
    result=$(($1 + $2))
    echo $result
}

sum=$(calculate_sum 5 10)
echo "Sum: $sum"
```

**Example with return:**
```bash
#!/bin/bash
is_even() {
    if [ $(($1 % 2)) -eq 0 ]
    then
        return 0  # True
    else
        return 1  # False
    fi
}

if is_even 4
then
    echo "Even number"
else
    echo "Odd number"
fi
```
