# Bash Cheat Sheet

## Command History
| Command | Description |
|---------|-------------|
| `!!` | Run the last command |
| `touch foo.sh` <br> `chmod +x !$` | `!$` represents the last argument of the last command (i.e., `foo.sh`) |

## Navigating Directories
| Command | Description |
|---------|-------------|
| `pwd` | Print current directory path |
| `ls` | List directories |
| `ls -a` | List directories including hidden files |
| `ls -l` | List directories in long form |
| `ls -l -h` | List directories in long form with human-readable sizes |
| `ls -t` | List directories by modification time, newest first |
| `stat foo.txt` | Show size, created and modified timestamps for a file |
| `tree` | Show directory and file tree |
| `cd foo` | Go to `foo` sub-directory |
| `cd` or `cd ~` | Go to home directory |
| `cd -` | Go to the last directory |
| `pushd foo` | Go to `foo` and push current directory to stack |
| `popd` | Return to the last directory in stack |

## Creating Directories
| Command | Description |
|---------|-------------|
| `mkdir foo` | Create a directory |
| `mkdir foo bar` | Create multiple directories |
| `mkdir -p foo/bar` | Create nested directories |
| `mktemp -d` | Create a temporary directory |

## Moving Directories
| Command | Description |
|---------|-------------|
| `cp -R foo bar` | Copy directory |
| `mv foo bar` | Move directory |
| `rsync -avz /foo /bar` | Copy directory with compression |
| `rsync -avz username@hostname:/foo /bar` | Copy remote directory to local |

## Deleting Directories
| Command | Description |
|---------|-------------|
| `rmdir foo` | Delete empty directory |
| `rm -r foo` | Delete directory including contents |
| `rm -rf foo` | Force delete directory |

## Creating Files
| Command | Description |
|---------|-------------|
| `touch foo.txt` | Create or update timestamp of file |
| `touch {foo,bar}.txt` | Create multiple files |
| `mktemp` | Create a temporary file |

## Standard I/O Redirection
| Command | Description |
|---------|-------------|
| `echo "foo" > bar.txt` | Overwrite file with content |
| `echo "foo" >> bar.txt` | Append content to file |
| `ls 1> stdout.txt` | Redirect stdout to a file |
| `ls 2> stderror.txt` | Redirect stderr to a file |
| `ls > /dev/null` | Discard output |
| `read foo` | Read input and store in `foo` |

## Moving Files
| Command | Description |
|---------|-------------|
| `cp foo.txt bar.txt` | Copy file |
| `mv foo.txt bar.txt` | Move file |
| `rsync -avz /foo.txt /bar.txt` | Copy file quickly if not changed |

## Deleting Files
| Command | Description |
|---------|-------------|
| `rm foo.txt` | Delete file |
| `rm -f foo.txt` | Force delete file |

## Reading Files
| Command | Description |
|---------|-------------|
| `cat foo.txt` | Print all contents |
| `less foo.txt` | View file in pages |
| `head foo.txt` | Print top 10 lines |
| `tail foo.txt` | Print bottom 10 lines |
| `wc foo.txt` | Count lines, words, and characters |

## File Permissions
### Permission Levels
| Number | Permission | rwx Representation |
|--------|-----------|------------------|
| 7 | Read, write, execute | `rwx` |
| 6 | Read, write | `rw-` |
| 5 | Read, execute | `r-x` |
| 4 | Read | `r--` |
| 3 | Write, execute | `-wx` |
| 2 | Write | `-w-` |
| 1 | Execute | `--x` |
| 0 | No permission | `---` |

### Common Permission Sets
| User | Group | Others | Description |
|------|-------|--------|-------------|
| 6 | 4 | 4 | User can read/write, others can read (default for files) |
| 7 | 5 | 5 | User can read/write/execute, others can read/execute (default for directories) |

### Changing File Permissions
| Command | Description |
|---------|-------------|
| `ls -l /foo.sh` | List file permissions |
| `chmod +100 foo.sh` | Add execute permission for user |
| `chmod u+x foo.sh` | Give user execute permission |
| `chmod g+x foo.sh` | Give group execute permission |
| `chmod a+x foo.sh` | Give everyone execute permission |
| `chmod u-x,g-x foo.sh` | Remove execute permission for user & group |
| `chmod 755 foo.sh` | Set permission to `rwxr-xr-x` |

This cheat sheet provides essential Bash commands with examples, formatted in a structured table format for easy reference. 🚀

# Bash Cheat Sheet

## Finding Files

| Command | Description |
|---------|-------------|
| `type wget` | Find the binary |
| `which wget` | Find the binary |
| `whereis wget` | Find the binary, source, and manual pages |
| `updatedb` | Update the `locate` index |
| `locate foo.txt` | Find a file |
| `locate --ignore-case` | Find a file (case insensitive) |
| `locate f*.txt` | Find a text file starting with 'f' |

### Using `find` (Slower but does not use an index)

| Command | Description |
|---------|-------------|
| `find /path -name foo.txt` | Find a file |
| `find /path -iname foo.txt` | Find a file (case insensitive) |
| `find /path -name "*.txt"` | Find all text files |
| `find /path -name foo.txt -delete` | Find and delete a file |
| `find /path -name "*.png" -exec pngquant {} \;` | Find all `.png` files and execute `pngquant` on them |
| `find /path -type f -name foo.txt` | Find a file |
| `find /path -type d -name foo` | Find a directory |
| `find /path -type l -name foo.txt` | Find a symbolic link |
| `find /path -type f -mtime +30` | Find files not modified in the last 30 days |
| `find /path -type f -mtime +30 -delete` | Delete files not modified in the last 30 days |

## Finding Text in Files (`grep`)

| Command | Description |
|---------|-------------|
| `grep 'foo' /bar.txt` | Search for 'foo' in a file |
| `grep -r 'foo' /bar` | Search for 'foo' in a directory recursively |
| `grep -R 'foo' /bar` | Search for 'foo' in a directory and follow symbolic links |
| `grep -l 'foo' /bar` | Show only files that contain 'foo' |
| `grep -L 'foo' /bar` | Show only files that do not contain 'foo' |
| `grep -i 'foo' /bar` | Case-insensitive search |
| `grep -x 'foo' /bar` | Match entire lines only |
| `grep -C 1 'foo' /bar` | Show 1 line of context before and after match |
| `grep -v 'foo' /bar` | Show lines that do not match 'foo' |
| `grep -c 'foo' /bar` | Count occurrences of 'foo' |
| `grep -n 'foo' /bar` | Show line numbers for matches |
| `grep --color 'foo' /bar` | Highlight matches in color |
| `grep -E 'foo|bar' /baz -R` | Use extended regular expressions (alternative: `egrep 'foo|bar' /baz -R`) |

## Replacing Text in Files (`sed`)

| Command | Description |
|---------|-------------|
| `sed 's/fox/bear/g' foo.txt` | Replace 'fox' with 'bear' in `foo.txt` (output to console) |
| `sed 's/fox/bear/gi' foo.txt` | Replace 'fox' with 'bear' (case insensitive) |
| `sed 's/red fox/blue bear/g' foo.txt` | Replace multiple words |
| `sed 's/fox/bear/g' foo.txt > bar.txt` | Save the changes to `bar.txt` |
| `sed -i 's/fox/bear/g' foo.txt` | Replace text and overwrite the original file |

## Symbolic Links (`ln`)

| Command | Description |
|---------|-------------|
| `ln -s foo bar` | Create a symbolic link `bar` pointing to `foo` |
| `ln -sf foo bar` | Overwrite an existing symbolic link |
| `ls -l` | Show where symbolic links are pointing |

## Compressing Files

### Using `zip`

| Command | Description |
|---------|-------------|
| `zip foo.zip /bar.txt` | Compress `bar.txt` into `foo.zip` |
| `zip foo.zip /bar.txt /baz.txt` | Compress multiple files |
| `zip foo.zip /{bar,baz}.txt` | Compress using brace expansion |
| `zip -r foo.zip /bar` | Compress an entire directory |

### Using `gzip`

| Command | Description |
|---------|-------------|
| `gzip /bar.txt` | Compress `bar.txt` into `bar.txt.gz` and delete the original file |
| `gzip -k /bar.txt` | Compress `bar.txt` but keep the original file |

### Using `tar`

| Command | Description |
|---------|-------------|
| `tar -czf foo.tgz /bar.txt /baz.txt` | Compress files into a `.tgz` archive |
| `tar -czf foo.tgz /{bar,baz}.txt` | Compress using brace expansion |
| `tar -czf foo.tgz /bar` | Compress an entire directory |

## Decompressing Files

| Command | Description |
|---------|-------------|
| `unzip foo.zip` | Extract a `.zip` file |
| `gunzip foo.gz` | Decompress a `.gz` file and remove the original |
| `gunzip -k foo.gz` | Decompress a `.gz` file but keep the original |
| `tar -xzf foo.tar.gz` | Extract a `.tar.gz` archive |
| `tar -xf foo.tar` | Extract a `.tar` archive |

## Disk Usage

| Command | Description |
|---------|-------------|
| `df` | Show disk space usage |
| `df -h` | Show human-readable disk space usage |
| `du` | Show directory and file sizes |
| `du /foo/bar` | Show size of a specific directory |
| `du -h` | Show human-readable file sizes |
| `du -d 1` | Show size of directories up to a depth of 1 |

---

This table makes the cheat sheet easy to read and copy-paste into a GitHub README. Let me know if you want any modifications! 🚀

Memory Usage
free                   # Show memory usage
free -h|--human        # Show human readable memory usage
free -h|--human --si   # Show human readable memory usage in power of 1000 instead of 1024
free -s|--seconds 5    # Show memory usage and update continuously every five seconds
Packages
apt update                   # Refreshes repository index
apt search wget              # Search for a package
apt show wget                # List information about the wget package
apt list --all-versions wget # List all versions of the package
apt install wget             # Install the latest version of the wget package
apt install wget=1.2.3       # Install a specific version of the wget package
apt remove wget              # Removes the wget package
apt upgrade                  # Upgrades all upgradable packages
Shutdown and Reboot
shutdown                     # Shutdown in 1 minute
shutdown now "Cya later"     # Immediately shut down
shutdown +5 "Cya later"      # Shutdown in 5 minutes

shutdown --reboot            # Reboot in 1 minute
shutdown -r now "Cya later"  # Immediately reboot
shutdown -r +5 "Cya later"   # Reboot in 5 minutes

shutdown -c                  # Cancel a shutdown or reboot

reboot                       # Reboot now
reboot -f                    # Force a reboot
Identifying Processes
top                    # List all processes interactively
htop                   # List all processes interactively
ps all                 # List all processes
pidof foo              # Return the PID of all foo processes

CTRL+Z                 # Suspend a process running in the foreground
bg                     # Resume a suspended process and run in the background
fg                     # Bring the last background process to the foreground
fg 1                   # Bring the background process with the PID to the foreground

sleep 30 &             # Sleep for 30 seconds and move the process into the background
jobs                   # List all background jobs
jobs -p                # List all background jobs with their PID

lsof                   # List all open files and the process using them
lsof -itcp:4000        # Return the process listening on port 4000
Process Priority
Process priorities go from -20 (highest) to 19 (lowest).

nice -n -20 foo        # Change process priority by name
renice 20 PID          # Change process priority by PID
ps -o ni PID           # Return the process priority of PID
Killing Processes
CTRL+C                 # Kill a process running in the foreground
kill PID               # Shut down process by PID gracefully. Sends TERM signal.
kill -9 PID            # Force shut down of process by PID. Sends SIGKILL signal.
pkill foo              # Shut down process by name gracefully. Sends TERM signal.
pkill -9 foo           # force shut down process by name. Sends SIGKILL signal.
killall foo            # Kill all process with the specified name gracefully.
Date & Time
date                   # Print the date and time
date --iso-8601        # Print the ISO8601 date
date --iso-8601=ns     # Print the ISO8601 date and time

time tree              # Time how long the tree command takes to execute
Scheduled Tasks
   *      *         *         *           *
Minute, Hour, Day of month, Month, Day of the week
crontab -l                 # List cron tab
crontab -e                 # Edit cron tab in Vim
crontab /path/crontab      # Load cron tab from a file
crontab -l > /path/crontab # Save cron tab to a file

* * * * * foo              # Run foo every minute
*/15 * * * * foo           # Run foo every 15 minutes
0 * * * * foo              # Run foo every hour
15 6 * * * foo             # Run foo daily at 6:15 AM
44 4 * * 5 foo             # Run foo every Friday at 4:44 AM
0 0 1 * * foo              # Run foo at midnight on the first of the month
0 0 1 1 * foo              # Run foo at midnight on the first of the year

at -l                      # List scheduled tasks
at -c 1                    # Show task with ID 1
at -r 1                    # Remove task with ID 1
at now + 2 minutes         # Create a task in Vim to execute in 2 minutes
at 12:34 PM next month     # Create a task in Vim to execute at 12:34 PM next month
at tomorrow                # Create a task in Vim to execute tomorrow
HTTP Requests
curl https://example.com                               # Return response body
curl -i|--include https://example.com                  # Include status code and HTTP headers
curl -L|--location https://example.com                 # Follow redirects
curl -o|--remote-name foo.txt https://example.com      # Output to a text file
curl -H|--header "User-Agent: Foo" https://example.com # Add a HTTP header
curl -X|--request POST -H "Content-Type: application/json" -d|--data '{"foo":"bar"}' https://example.com # POST JSON
curl -X POST -H --data-urlencode foo="bar" http://example.com                           # POST URL Form Encoded

wget https://example.com/file.txt .                            # Download a file to the current directory
wget -O|--output-document foo.txt https://example.com/file.txt # Output to a file with the specified name
Network Troubleshooting
ping example.com            # Send multiple ping requests using the ICMP protocol
ping -c 10 -i 5 example.com # Make 10 attempts, 5 seconds apart

ip addr                     # List IP addresses on the system
ip route show               # Show IP addresses to router

netstat -i|--interfaces     # List all network interfaces and in/out usage
netstat -l|--listening      # List all open ports

traceroute example.com      # List all servers the network traffic goes through

mtr -w|--report-wide example.com                                    # Continually list all servers the network traffic goes through
mtr -r|--report -w|--report-wide -c|--report-cycles 100 example.com # Output a report that lists network traffic 100 times

nmap 0.0.0.0                # Scan for the 1000 most common open ports on localhost
nmap 0.0.0.0 -p1-65535      # Scan for open ports on localhost between 1 and 65535
nmap 192.168.4.3            # Scan for the 1000 most common open ports on a remote IP address
nmap -sP 192.168.1.1/24     # Discover all machines on the network by ping'ing them
DNS
host example.com            # Show the IPv4 and IPv6 addresses

dig example.com             # Show complete DNS information

cat /etc/resolv.conf        # resolv.conf lists nameservers
Hardware
lsusb                  # List USB devices
lspci                  # List PCI hardware
lshw                   # List all hardware
Terminal Multiplexers
Start multiple terminal sessions. Active sessions persist reboots. tmux is more modern than screen.

tmux             # Start a new session (CTRL-b + d to detach)
tmux ls          # List all sessions
tmux attach -t 0 # Reattach to a session

screen           # Start a new session (CTRL-a + d to detach)
screen -ls       # List all sessions
screen -R 31166  # Reattach to a session

exit             # Exit a session
Secure Shell Protocol (SSH)
ssh hostname                 # Connect to hostname using your current user name over the default SSH port 22
ssh -i foo.pem hostname      # Connect to hostname using the identity file
ssh user@hostname            # Connect to hostname using the user over the default SSH port 22
ssh user@hostname -p 8765    # Connect to hostname using the user over a custom port
ssh ssh://user@hostname:8765 # Connect to hostname using the user over a custom port
Set default user and port in ~/.ssh/config, so you can just enter the name next time:

$ cat ~/.ssh/config
Host name
  User foo
  Hostname 127.0.0.1
  Port 8765
$ ssh name
Secure Copy
scp foo.txt ubuntu@hostname:/home/ubuntu # Copy foo.txt into the specified remote directory
Bash Profile
bash - .bashrc
zsh - .zshrc
# Always run ls after cd
function cd {
  builtin cd "$@" && ls
}

# Prompt user before overwriting any files
alias cp='cp --interactive'
alias mv='mv --interactive'
alias rm='rm --interactive'

# Always show disk usage in a human readable format
alias df='df -h'
alias du='du -h'
Bash Script
Variables
#!/bin/bash

foo=123                # Initialize variable foo with 123
declare -i foo=123     # Initialize an integer foo with 123
declare -r foo=123     # Initialize readonly variable foo with 123
echo $foo              # Print variable foo
echo ${foo}_'bar'      # Print variable foo followed by _bar
echo ${foo:-'default'} # Print variable foo if it exists otherwise print default

export foo             # Make foo available to child processes
unset foo              # Make foo unavailable to child processes
Environment Variables
#!/bin/bash

env            # List all environment variables
echo $PATH     # Print PATH environment variable
export FOO=Bar # Set an environment variable
Functions
#!/bin/bash

greet() {
  local world = "World"
  echo "$1 $world"
  return "$1 $world"
}
greet "Hello"
greeting=$(greet "Hello")
Exit Codes
#!/bin/bash

exit 0   # Exit the script successfully
exit 1   # Exit the script unsuccessfully
echo $?  # Print the last exit code
Conditional Statements
Boolean Operators
$foo - Is true
!$foo - Is false
Numeric Operators
-eq - Equals
-ne - Not equals
-gt - Greater than
-ge - Greater than or equal to
-lt - Less than
-le - Less than or equal to
-e foo.txt - Check file exists
-z foo - Check if variable exists
String Operators
= - Equals
== - Equals
-z - Is null
-n - Is not null
< - Is less than in ASCII alphabetical order
> - Is greater than in ASCII alphabetical order
If Statements
#!/bin/bash

if [[$foo = 'bar']]; then
  echo 'one'
elif [[$foo = 'bar']] || [[$foo = 'baz']]; then
  echo 'two'
elif [[$foo = 'ban']] && [[$USER = 'bat']]; then
  echo 'three'
else
  echo 'four'
fi
Inline If Statements
#!/bin/bash

[[ $USER = 'rehan' ]] && echo 'yes' || echo 'no'
While Loops
#!/bin/bash

declare -i counter
counter=10
while [$counter -gt 2]; do
  echo The counter is $counter
  counter=counter-1
done
For Loops
#!/bin/bash

for i in {0..10..2}
  do
    echo "Index: $i"
  done

for filename in file1 file2 file3
  do
    echo "Content: " >> $filename
  done

for filename in *;
  do
    echo "Content: " >> $filename
  done
Case Statements
#!/bin/bash

echo "What's the weather like tomorrow?"
read weather

case $weather in
  sunny | warm ) echo "Nice weather: " $weather
  ;;
  cloudy | cool ) echo "Not bad weather: " $weather
  ;;
  rainy | cold ) echo "Terrible weather: " $weather
  ;;
  * ) echo "Don't understand"
  ;;
esac
