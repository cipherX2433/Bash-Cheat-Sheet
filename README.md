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


| **Category**            | **Command**                              | **Description** |
|------------------------|--------------------------------------|----------------|
| **Memory Usage**      | `free`                               | Show memory usage |
|                        | `free -h`                           | Show human-readable memory usage |
|                        | `free -h --si`                      | Show memory usage in power of 1000 instead of 1024 |
|                        | `free -s 5`                         | Show memory usage and update every 5 seconds |
| **Package Management** | `apt update`                        | Refresh repository index |
|                        | `apt search wget`                   | Search for a package |
|                        | `apt show wget`                     | Show package details |
|                        | `apt list --all-versions wget`      | List all versions of a package |
|                        | `apt install wget`                  | Install the latest version of a package |
|                        | `apt install wget=1.2.3`            | Install a specific version of a package |
|                        | `apt remove wget`                   | Remove a package |
|                        | `apt upgrade`                       | Upgrade all packages |
| **Shutdown & Reboot**  | `shutdown`                          | Shutdown in 1 minute |
|                        | `shutdown now "Cya later"`         | Shutdown immediately |
|                        | `shutdown +5 "Cya later"`          | Shutdown in 5 minutes |
|                        | `shutdown --reboot`                 | Reboot in 1 minute |
|                        | `shutdown -r now "Cya later"`      | Reboot immediately |
|                        | `shutdown -r +5 "Cya later"`       | Reboot in 5 minutes |
|                        | `shutdown -c`                       | Cancel a shutdown/reboot |
|                        | `reboot`                            | Reboot now |
| **Process Management** | `top`                                | Show running processes interactively |
|                        | `htop`                               | Enhanced process viewer |
|                        | `ps all`                             | List all processes |
|                        | `pidof foo`                          | Get PID of a process |
|                        | `CTRL+Z`                             | Suspend foreground process |
|                        | `bg`                                 | Resume suspended process in background |
|                        | `fg`                                 | Bring background process to foreground |
|                        | `jobs`                               | List background jobs |
|                        | `kill PID`                           | Terminate process by PID |
|                        | `kill -9 PID`                        | Force kill process by PID |
|                        | `pkill foo`                          | Kill process by name |
|                        | `pkill -9 foo`                       | Force kill process by name |
| **Date & Time**        | `date`                               | Show current date and time |
|                        | `date --iso-8601`                   | Show date in ISO 8601 format |
| **Scheduled Tasks**    | `crontab -l`                         | List scheduled cron jobs |
|                        | `crontab -e`                         | Edit cron jobs |
| **Network Tools**      | `ping example.com`                   | Send ping requests |
|                        | `ip addr`                            | Show IP addresses |
|                        | `netstat -l`                         | List open ports |
|                        | `traceroute example.com`            | Trace network route |
|                        | `nmap 0.0.0.0`                      | Scan open ports |
| **SSH & Secure Copy**  | `ssh user@hostname`                 | Connect to a remote server |
|                        | `scp file.txt user@hostname:/dir`  | Securely copy file to a remote system |
| **Terminal Multiplexers** | `tmux`                            | Start a tmux session |
|                        | `tmux ls`                           | List tmux sessions |
|                        | `screen`                            | Start a screen session |
| **Hardware Info**      | `lsusb`                              | List USB devices |
|                        | `lspci`                              | List PCI devices |
|                        | `lshw`                               | Show all hardware info |


| Command | Description |
|---------|-------------|
| **tmux** | Start a new tmux session (`CTRL-b + d` to detach) |
| `tmux ls` | List all tmux sessions |
| `tmux attach -t 0` | Reattach to a tmux session |
| **screen** | Start a new screen session (`CTRL-a + d` to detach) |
| `screen -ls` | List all screen sessions |
| `screen -R 31166` | Reattach to a screen session |
| `exit` | Exit a session |

### Secure Shell Protocol (SSH)
| Command | Description |
|---------|-------------|
| `ssh hostname` | Connect to hostname using your current user name over the default SSH port (22) |
| `ssh -i foo.pem hostname` | Connect to hostname using the identity file |
| `ssh user@hostname` | Connect to hostname using the user over the default SSH port (22) |
| `ssh user@hostname -p 8765` | Connect to hostname using the user over a custom port |
| `ssh ssh://user@hostname:8765` | Connect to hostname using the user over a custom port |

### Secure Copy (SCP)
| Command | Description |
|---------|-------------|
| `scp foo.txt ubuntu@hostname:/home/ubuntu` | Copy `foo.txt` into the specified remote directory |

### Bash Profile
| Command | Description |
|---------|-------------|
| `bash - .bashrc` | Load `.bashrc` file |
| `zsh - .zshrc` | Load `.zshrc` file |
| `alias cp='cp --interactive'` | Prompt before overwriting files when copying |
| `alias mv='mv --interactive'` | Prompt before overwriting files when moving |
| `alias rm='rm --interactive'` | Prompt before deleting files |
| `alias df='df -h'` | Show disk usage in a human-readable format |
| `alias du='du -h'` | Show directory size in a human-readable format |
| `function cd { builtin cd "$@" && ls; }` | Run `ls` automatically after `cd` |

### Bash Scripting
#### Variables
| Command | Description |
|---------|-------------|
| `foo=123` | Initialize variable `foo` with `123` |
| `declare -i foo=123` | Declare `foo` as an integer |
| `declare -r foo=123` | Declare `foo` as a readonly variable |
| `export foo` | Make `foo` available to child processes |
| `unset foo` | Remove `foo` from the environment |

#### Environment Variables
| Command | Description |
|---------|-------------|
| `env` | List all environment variables |
| `echo $PATH` | Print `PATH` environment variable |
| `export FOO=Bar` | Set an environment variable |

#### Functions
| Command | Description |
|---------|-------------|
| `greet() { echo "Hello $1"; }` | Define a function `greet` that takes an argument |
| `greet "World"` | Call the `greet` function |

#### Exit Codes
| Command | Description |
|---------|-------------|
| `exit 0` | Exit the script successfully |
| `exit 1` | Exit the script unsuccessfully |
| `echo $?` | Print the last exit code |

### Conditional Statements
#### Boolean Operators
| Operator | Description |
|---------|-------------|
| `$foo` | Is true |
| `!$foo` | Is false |

#### Numeric Operators
| Operator | Description |
|---------|-------------|
| `-eq` | Equals |
| `-ne` | Not equals |
| `-gt` | Greater than |
| `-ge` | Greater than or equal to |
| `-lt` | Less than |
| `-le` | Less than or equal to |
| `-e foo.txt` | Check if file exists |
| `-z foo` | Check if variable exists |

#### String Operators
| Operator | Description |
|---------|-------------|
| `=` | Equals |
| `==` | Equals |
| `-z` | Is null |
| `-n` | Is not null |
| `<` | Less than (ASCII order) |
| `>` | Greater than (ASCII order) |

#### If Statements
```bash
if [[ $foo = 'bar' ]]; then
  echo 'one'
elif [[ $foo = 'bar' ]] || [[ $foo = 'baz' ]]; then
  echo 'two'
elif [[ $foo = 'ban' ]] && [[ $USER = 'bat' ]]; then
  echo 'three'
else
  echo 'four'
fi
```

#### Inline If Statements
```bash
[[ $USER = 'rehan' ]] && echo 'yes' || echo 'no'
```

### Loops
#### While Loop
```bash
declare -i counter
counter=10
while [[ $counter -gt 2 ]]; do
  echo "The counter is $counter"
  counter=$((counter-1))
done
```

#### For Loops
```bash
for i in {0..10..2}; do
  echo "Index: $i"
done

for filename in file1 file2 file3; do
  echo "Content: " >> $filename
done

for filename in *; do
  echo "Content: " >> $filename
done
```

### Case Statements
```bash
echo "What's the weather like tomorrow?"
read weather

case $weather in
  sunny | warm ) echo "Nice weather: $weather" ;;
  cloudy | cool ) echo "Not bad weather: $weather" ;;
  rainy | cold ) echo "Terrible weather: $weather" ;;
  * ) echo "Don't understand" ;;
esac
```


