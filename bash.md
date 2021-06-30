# Bash

Default shell: `/bin/zsh`

Switch to a bash sub shell on demand:

```sh
bash
```

_(`exit` to return to default)_

Change default shell (to bash):

```sh
chsh -s /bin/bash
```

## shell

A command line interpreter that interprets the commands you type in your terminal and passes them on to the operating system.

The purpose of the shell is to make it more convenient for you to issue commands to your computer.

## bash

Bash is a type of shell. (Bourne Again Shell). The most commonly used Linux shell today. It is fast and has a broad set of features.

## script

A file containing a series of commands that will be run by the shell. Scripts make automating sets of commands very convenient. They save you time and make you more productive.

## shell expansions

Powerful features that allow us to retrieve data, process command output, and perform calculations.

## parameter

Any entity that stores values. There are 3 types of shell parameters (Variables, positional parameters, special parameters).

# Basics

All bash scripts have 3 core components:

1. The shebang line

   Tells the shell what type of script we are writing (bash/python/etc).

   This should be the absolute path to the (latest) bash interpreter

   ```
   #!/usr/local/bin/bash
   ```

2. Commands

   ```sh
   echo “This is my first script”
   ```

3. Exit statement

   The exit code tells the shell whether the script ran successfully or unsuccessfully. (0=successful, 1-255 = unsuccessful)

   ```sh
   exit 0
   ```

Before running a script it must be given execute permissions. _See_ [Setting Up Secure Permissions](#permissions)

```sh
chmod +x <filename>
```

> Comments in bash
>
> ```sh
> # Commented line
> ```

There are 5 professional components of a bash script:

```sh
# Author

# Date created

# Last Modified

# Description:

# Usage:
```

> Current User's Home directory: `~` _or_ `$HOME`

# Setting Up Permissions <a name="permissions"></a>

## **d**|**rwx**|**rwx**|**rwx**|

### - / d

file / directory

### rwx / -

read / write / execute (or '-' = no permission)

\*(The 3 sets of rwx code represent the access permissions for **user** | **group** | **all**).

An **octal number** is made up of 3 numeric values that represent the access permissions for each set.

| no. | code |
| --- | ---- |
| 0   | -    |
| 4   | r--  |
| 5   | r-x  |
| 6   | rw-  |
| 7   | rwx  |

[Reference: Permissions Calculator][octal-codes]

Set permissions for a file

```sh
chmod <octal number> <filename>
```

eg.

```sh
chmod 744 my_first_script.sh
```

# Systems Path

The systems path is a variable `($PATH)`. It references a list of directories that should be known to the shell so that when a filename is written in the shell as a command, the shell knows within which folders to search for executable files.

A directory can be added to the path variable by amending the .zshrc file in the users root folder:

```sh
export PATH=“$PATH:$HOME/bash_course/scripts”
```

[ How to add to the shell path using macOS ][macos-shell-path]

# Variables

(User defined variable eg:)

```sh
name=name
```

_(lowercase variable name & no spaces!)_

## Shell Variables

Pre-defined variables that have particular meaning in the bash shell

## Bourne (and bash) shell variables:

Stores all the directories the shell should search for executable files as command names

```sh
echo $PATH
```

Stores the absolute path to the current user’s home directory and is the default for the cd builtin command.

```sh
echo $HOME
```

The username of the current user

```sh
$USER
```

The name of the current host, the name that the user has given to their computer

```sh
$HOSTNAME
```

“Prompt stream 1” The prompt string shown in the terminal before each command

```sh
$PS1
```

A string describing the machine Bash is running on or processor architecture the computer is running on

```sh
$HOSTTYPE
```

# Parameter Expansion

Parameter expansion is used to retrieve the value stored
in a parameter

### Example:

```sh
name=“Fran DeBoo”
```

Convert the first letter to lowercase:

```sh
echo ${name,}
```

_output: fran DeBoo_

Convert the entire string to lowercase:

```sh
echo ${name,,}
```

_output: fran deboo_

Convert the first letter to uppercase:

```sh
echo ${name^}
```

_output: Fran DeBoo_

Convert the entire string to uppercase:

```sh
echo ${name^^}
```

_output: FRAN DEBOO_

Return the number of characters in a string:

```sh
`echo ${#name}
```

_output: 10_

Return a 'slice' of a string starting at the character number defined by “offset” and expand up to a length
of “length”

```sh
${parameter:offset:length}
```

### Example:

```sh
numbers=0123456789
```

`echo ${numbers:0:7}`

_output: 0123456789_

`echo ${numbers:1:5}`

_output: 12345_

`echo ${numbers:3}`

_output: 3_

`echo ${numbers:3:}`

_output:_

`echo ${numbers: -3:5}`

_output:_

[Reference: Bad Subsitition Error][bad-substitution]

[Reference: Bash and Zsh][bash-zsh]

[Reference: zsh Modifiers][zsh-modifiers]

# Command Substitution

Command substitution is a shell feature that allows you to grab the output of a command and do stuff with it- for example, save data in user-defined variables.

Command substitution syntax:

```sh
$(command)
```

# Arithmetic Expansion

Arithmetic expansion syntax:

```sh
$((expression))
```

### Example:

`echo ${(4 + 2)}`

_output: 6_

`echo ${(4 - 2)}`

_output: 2_

`echo ${(4 / 2)}`

_output: 2_

`echo ${(4 * 2)}`

_output: 8_

`echo ${(4 ** 2)}`

_output: 16_

`echo ${(5 % 2)}`

_output: 6_

Enter basic calculator:

```sh
bc
```

Use basic calculator inline:

```sh
echo “5/2” | bc
```

Set the bc’s internal scale variable to determine the number of decimal places in the output:

```sh
echo “scale=2; 5/2” | bc
```

# Tilde Expansion ~

```sh
$HOME or ~
```

Current active directory:

```sh
$PWD or ~+
```

Previous active directory:

```sh
$OLDPWD or ~-
```

# Brace Expansion

Expand out string list:

```sh
echo {jan,feb,mar,apr,may}
```

_output: jan feb mar apr may_

Expand out range list:

```sh
foo@bar:~$ echo {1..10}
```

_(output: 1 2 3 4 5 6 7 8 9 10)_

### Example:

`echo {10..1}`
_(output: 10 9 8 7 6 5 4 3 2 1)_

`echo {a..z}`
_output: a b c d e f g h I j k l m n o p q r s t u v w x y z_

Expand in given steps:

```sh
echo {1..10..3}
```

_output: 1 4 7 10_

### Example:

Make directories for every month of the year:

```
mkdir month{01..12}
```

Create files for every day of the month in every month directory for the year:

```sh
touch month{01..12}/day{01..31}.txt
```

# How Bash Processes Command Lines

Bash goes through a 5 step process to interpret the command and decide what to do with it. At the end of the 5 steps, the left over command is executed.

## Step 1: Tokenisation

Breaks the command into Tokens and distinguishes between Words and Operators

### Token

A sequence of characters that is considered as a single unit by the shell.

### Metacharacters

Special characters:

- Space (‘ ’)
- Tab (\t)
- New Line (\n)
- **|**
- **&**
- **;**
- **(** _and_ **)**
- **<** _and_ **>**

### Words

A token that does not contain an unquoted metacharacter.

### Operators

Tokens that contain at least one unquoted metacharacters. There are two types of operators- control operators and redirection operators.

## Step 2: Command Identification

Breaks the command line up into either simple or compound commands

### Simple Commands

A list of words separated by spaces and terminated by wither a new line or one of the other control operators available in bash. The first word of a simple command is interpreted as the command name, and the following words are interpreted as the arguments to that command.

### Compound Commands

Compound commands are essentially bash’s programming constructs. Each compound command starts with a reserved word and is terminated by a corresponding reserved word.

```sh
if [[ 2 -gt 1 ]]; then
    echo “hello world”
fi
```

## Step 3: Expansions

There are four stages of expansion:

1. Brace Expansion

2. - Parameter Expansion `$(variable^)`
   - Arithmetic Expansion `${(4 + 2)}`
   - Command Substitution `$((command))`
   - Tilde Expansion `~+`

3. Word Splitting

   Word Splitting is a process the shell performs to split the result of some unquoted expansions into separate words. Word splitting is only performed on the results of unquoted:

   - Parameter expansions

   - Command substitutions

   - Arithmetic expansions

   Expansions in earlier stages have a higher precedence than expansions in later stages and are therefore performed first. They are performed in order.

   The `$IFS` shell variable defines “ \t\n” as separators for words (space/tab/new line)

   Creates separate files for each number:

   ```sh
   numbers=1 2 3 4 5
   touch $numbers
   ls
   ```

   _output: 1 2 3 4 5_

   > If you want the output of a Parameter expansion / Arithmetic expansion / Command Substitution …to be considered as a single word: wrap that expansion in double quotes!

4. Globbing aka file name expansion

   - Writing filtering commands in shorthand.
   - Only performed on words .
   - Generates an alphabetically sorted list of files that match the given pattern exactly
   - Scans words for unquoted special characters ( \* ? [ )
   - Performs ‘Globbing’ on words that contain a special pattern character

   List all files that end with .txt in current directory:

   ```sh
   ls *.txt
   ```

   List all files that start with file and end in .txt in current directory:

   ```sh
   file*.txt
   ```

   _output: file1.txt file123.txt file2.txt file3.txt filea.txt fileabc.txt fileb.txt filec.txt_

   List all files that start with file and one unknown character:

   ```sh
   file?.txt
   ```

   _output: file1.txt file2.txt file3.txt_

   List all files that start with file and any character between a-g:

   ```sh
   file[a-g].txt
   ```

   _output: filea.txt fileb.txt filec.txt_

## Step 4: Quote Removal

Removes all supportive quotes;- unquoted backslashes. Single quote characters and double quote characters that did not result from a shell expansion. These help to express the command as required as they protect reserved characters from default behaviours. They quotes are not part of the command and so are removed

## Step 5: Redirections

Processes any redirection operators that are on the command line (>). Linux and other unix-derived systems allow commands to take advantage of three standard data streams.

Stream 0 = Standard Input (`stdin`)
Provides us with an alternative way of providing input to a command, aside from using command line arguments.

Stream 1 = Standard Output (`stdout`)
Contains the data that is produces after a successful command execution

Stream 2 = Standard Error (`stderr`)
Contains all error messages and status messages that a command produces

Redirection is about changing where streams connects

| operator | description                                                      |
| -------: | ---------------------------------------------------------------- |
|      `>` | redirect a standard output                                       |
|     `2>` | redirect a standard error                                        |
|     `&>` | redirect both standard and standard error data                   |
|     `>>` | appends to data in the destination file rather than truncates it |

# Quoting

(protects reserved characters from default behaviours)

Removing special meanings from the 3 main characters. Three main characters are:

- (\\) - Removes special meaning from the character immediately following
- (‘ ‘) - Removes special meaning from any characters between the quotes
- (“ “) - Preserves the special meaning of $ and ` ` but removes special meaning of all other characters within the quotes

Quoting
Removing special meanings

# Positional Parameters

Command line arguments are information you give to your script from your command line. Each argument is separated by a space. Positional parameters are parameters set by the shell to store the value of each of these command line arguments.

Call a script with arguments:

```sh
myscript Fran $HOME blue
```

Refer to the positional parameters in the script:

```sh
#!/usr/local/bin/bash
echo “My name is $1”
echo “My home directory is $2”
echo “My favourite colour is $3”
```

> ### Special Parameters
>
> Parameters that bash gives special meaning. The value of a special parameter is calculated for us. The value of a special parameter cannot be modified.

Returns total number of positions parameters that have been provided to the script:

```sh
$#
```

Expands to the name of the current shell / script from where it is being called:

```sh
$0
```

Access all positional parameters provided to the script at once - provides all positional parameter as one word but separates them with the character defined the IFS variable):

```sh
“$\*”
```

Access all positional parameters provided to the script at once. The parameters are subject to word splitting and returned as unquoted separate words.

```sh
$\* $@ ie: $1 $2 $3 $4.. $n
```

Retain quotes given to multi-word parameters to protect the parameters from word splitting
“$@“ ie: “daily feedback” “monthly report”

# read

Requests input from the user and stores it in the `$REPLY` variable by default or any custom variables passed as parameters.

Define a prompt message to display to the user:

```sh
read -p “<message>: ”
```

Set a time limit for the user to return a response:

```sh
read -t <seconds>
```

Mask the input that the user provides so that it is not visible in the terminal:

```sh
read -s
```

Limits the user’s response to an exact number of characters:

```sh
read -N
```

Sets the maximum number of characters that the user can use:

```sh
read -n
```

# select

Presents the user with multiple options and saves their selection in the `$RESPONSE` variable by default or a custom variable name provided as a parameter

```sh
#!/usr/local/bin/bash
```

Define a prompt message to display to the user:

```sh
PS3= “What day of the week is it?”
```

Provide a variable name after select keyword followed by `in`

```sh
select weekday in mon tue wed thu fri sat sun;
do
```

End the looping of the select command

```sh
break
done
```

Set a time limit for the user to return a response:

```sh
read -t <seconds>
```

Mask the input that the user provides so that it is not visible in the terminal

```sh
read -s
```

# Chaining Commands

A list of commands is one or more commands on a given line

List operators are examples of **control operators**
|operator|description|
|-------:|-----------|
|`&`|run commands asynchronously|
|`;`|run synchronously and saves space in bash script|
|`&&`|makes it so that the second command only runs if the first command is successful (`exit 0`)|
|`||`|makes it so that the second command only runs if the first one failed|

## Ternary operator

CommandA `&&` CommandB `||` Command C
“Run CommandA- if successful run command B, if not run command C”

## test

A command that can be used in bash to compare different pieces of information.

If a test command is evaluated to be true, the test command will return an exit code of 0. Likewise if a test command is evaluated to be false the test command will return an exit code of 1.

true = 0
false = 1

### Test commands for numbers

Evaluates if 2 is equal to 2

```sh
[ 2 -eq 2 ] ; echo $?
```

Evaluates if 2 is not equal to 2

```sh
[ 2 -ne 2 ] ; echo $?
```

Greater than
-gt
Less than
-lt

Greater than or equal to
-geq

Less than or equal to
-leq

Test commands for strings
Evaluate if 2 strings are equal
= eg. [[$HOME = ~]] output: 0

Evaluate if 2 strings are not equal
!= [[$HOME != ~]] output: 1

Evaluate if a string is empty
-z eg. [[-z $c]] ; echo $? output: 0

Evaluate if a string is not empty
-n eg. [[-n $c]] ; echo $? output: 1

Test commands for files
Evaluate if a file exists
-e eg. [[-e today.txt]] ; echo $? output: 1

Test if a regular file
-f eg. [[-f today.txt]] ; echo $?

Test if a directory
-d eg. [[-d today.txt]] ; echo $? output: 1

Test if a file exists and has execution permissions
-x eg. [[-x script]] ; echo $?

if statements
if statements start and end using the reserved words ‘if’ and ‘fi’. If statements check the exit status of a command. If statements only run code ‘if’ a certain condition is true (exit status 0).
if [ 2 -eq 1 ]; then
echo test passed
elif [ 1 -eq 1 ]; then
echo second test passed
else
echo test failed
fi

Chaining test conditions in an if statement

#!/usr/local/bin/bash

a=$(cat file1.txt)
b=$(cat file2.txt)
c=$(cat file3.txt)

if [ $a = $b ] && [ $a = $c ]; then
rm file1.txt file2.txt
else
echo “Files do not match”
fi

# Case Statements

Offer an alternative was to create branching solutions. Case start and end using the reserved words ‘case’ and ’esac’. Case statements are a simpler form of the if;then/elif; then statement but the tradeoff is that there can only be logical checks on a single variable.

Provide a variable to work with. Provide $ and wrap inside double quotes to prevent word-splitting.

```sh
read -p “Provide a number between 0-999: ” number
```

Provide a variable name prepended with $ and wrapped in double quotes:

```sh
case “$number” in
```

Provide clauses (terminate a clause with a double ;;):

```sh
    [0-9])
        echo “you have entered a single digit number”
        ;;
    [0-9][0-9])
        echo “you have entered a two digit number”
        ;;
    [0-9][0-9][0-9])
        echo “you have entered a three digit number”
        ;;
```

Provide a default case in case no other patterns match:

```sh
    *)
        echo “you have entered a number that is more than three digits”
esac
```

# Arrays

```sh
numbers=(1 2 3 4)
```

_(spaces instead of commas to separate indices)_

0th element

1st element

2nd element

3rd element

Access the 3rd element

    ${numbers[2]}

Access all values in an array at once

    ${numbers[@]}

Access all values from 1 to the end with a length of 2

    ${numbers[@]:1:2}

Add 5 to the end of the array

    numbers+=(5)

Remove the 3rd element

    Unset numbers[2]

Reveal the indexes of the array elements

    ${!numbers}

Reassign an index value

    numbers[0]=a reassign an index value

# read-array

The readarray command converts whatever it reads on its standard input stream into an array. It creates an array with the contents of the file.

    readarray <arrayname> < file

(e.g) remove formatting characters such as ‘\n’ with `-t`:

    readarray -t days < days.txt

We cannot simply pipe to the readarray command because every command in a pipeline is run in its own subshell. The new array that the readarray command creates would exist within that sub shell.

# Process substitution

    readarray -t files < <(ls ~/bash_course/array)

# for loops

```sh
for <variable> in value1 value2 value3; do
    commands…
done
```

### Example:

```sh
readarray -t urls < urls.txt

for url in “${urls}”; do
    webname=$(echo “$url” | cut -d “.” -f 2)
    curl —head “$url” > “$webname”.txt
done
```

# at command

Quickly and easily schedule scripts to run at pre-scheduled times and dates. However the at command will only execute job if PC is on at the time and there is no way to set up recurring jobs.

Launch daemons (linux)

    service atd start

Launch daemons (macOS)

    sudo launchctl load -w /System/Library/LaunchDaemons/ssh.plist

Launch daemons (macOS) 2.0

    sudo launchctl bootstrap system -w /System/Library/LaunchDaemons/ssh.plist

Stop daemon (macOS) 2.0

    sudo launchctl bootout system -w /System/Library/LaunchDaemons/ssh.plist

List jobs to take place at a specific time:

    at 9:30am

Declare jobs in prompt:

    > echo “Hello World”

End the prompt/ list of commands

    Ctrl + D

Provide a file containing job list as input:

    at -f at_script.sh 10:35am

Remove a (specified) job from the job list:

    at -r <job id>

Alternative timestamp examples:

```sh
at -f at_script.sh 9am 23.07.2021
at -f at_script.sh 9am 24/07/2021
at -f at_script.sh 9am Monday
at -f at_script.sh 9am tomorrow
at -f at_script.sh 9am next week
at -f at_script.sh 9am now + 7 days
at -f at_script.sh 9am now + 5 mins
```

# Cron command

schedule your scripts to run on a repeated schedule but will only execute job if PC is on at the time.

Launch daemons (linux)

```sh
service cron start
```

# Cron directories

```sh
#!/usr/local/bin/bash

sudo apt -y update && sudo apt -y upgrade
reboot
```

# launchd

```sh
/Library/LaunchDaemons
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
	<dict>
		<key>Label</key>
		<string>com.example.app</string>
		<key>Program</key>
		<string>/Users/Me/Scripts/cleanup.sh</string>
		<key>RunAtLoad</key>
		<true/>
	</dict>
</plist>
```

[How to Use launchd to Run Services in macOS][macos-launchd]

[Reference: launchd and Daemons][launchd-info]

[YouTube: How to Use launchd to Schedule jobs on macOS][yt-launchd-macos]

[YouTube: De-mystifying launchd][yt-demystify-launchd]

# ssh

An ssh key is an encrypted certificate that is used to authenticate your ssh connection. A copy of the certificate is stored on the server and another copy is stored on your system. When you attempt to make an ssh connection to the server, the server compares it’s copy.

### Generate a ssh key

```sh
ssh-keygen
```

> ssh keys are saved in `~/.ssh/`

### Connect to a remote server

```sh
ssh @root<ip address>
```

If you have multiple SSH keys loaded into your agent, specify the key:

```sh
ssh -i ~/.ssh/id_rsa_digitalocean @root46.101.88.159
```

[Troubleshooting Permission denied (publickey) for root login][digitalocean-troubleshooting]

Copy a file from a local machine to remote server

```sh
scp <local/path/to/file> root@<ip address>:<save/path/remote>
```

### Example

```sh
scp ~/ @root46.101.88.159:~/
```

Copy a file from a remote server to local machine

```sh
scp root@<ip address>:<remote/path/to/file/> <save/path/locally>
```

### Example.

```sh
scp @root46.101.88.159:~/ ~/
```

<!-- Links -->

[digitalocean-troubleshooting]: https://www.digitalocean.com/community/questions/permission-denied-publickey-for-root-login
[bad-substitution]: https://hybriddbablog.com/2021/01/25/
[bash-zsh]: bash-bad-substitution-upgrade-your-bash-version/
[launchd-info]: https://www.launchd.info/
[macos-launchd]: https://medium.com/swlh/how-to-use-launchd-to-run-services-in-macos-b972ed1e352
[macos-shell-path]: https://wpbeaches.com/how-to-add-to-the-shell-path-in-macos-using-terminal/
[zsh-modifiers]: https://zsh.sourceforge.io/Doc/Release/Expansion.html#:~:text=%5B%20%3F%20%5D-,14.1.4,-Modifiers
[octal-codes]: http://permissions-calculator.org/
[yt-launchd-macos]: https://youtu.be/oIn75ZbmWrQ
[yt-demystify-launchd]: https://www.youtube.com/watch?v=guBV0jftT40&t=4s
