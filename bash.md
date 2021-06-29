# Bash
Default shell: /bin/zsh

Switch to a bash sub shell on demand: `bash` *(exit to return to default)*

Change default shell (to bash): `chsh -s /bin/bash`

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

`this is some code`


# Basics
+ All bash scripts have 3 core components:
  1. The shebang line
    
     Tells the shell what type of script we are writing (bash/python/etc).
     This should be the absolute path to the (latest) bash interpreter 
     
        `#!/usr/local/bin/bash`

  2. Commands
    
        `echo “This is my first script”`

  3. Exit statement
     
     The exit code tells the shell whether the script ran successfully or unsuccessfully. (0=successful, 1-255 = unsuccessful)
     
        `exit 0`

+ Before running a script it must be given execute permissions.
    
        chmod +x <filename>

+ Bash Comment
    
        # Commented line

+ Current User's Home directory:  `~` *or* `$HOME`

+ There are 5 professional components of a bash script:
    
        # Author
        
        # Date created
        
        # Last Modified
        
        # Description:
        
        # Usage:


# Setting Up Secure Permissions

## **d**|**rwx**|**rwx**|**rwx**|

## - / d

file / directory

## rwx / -

read / write / execute (or '-' = no permission)

*(The 3 sets of rwx code represent the access permissions for **user** | **group** | **all**).

An octal number is made up of 3 numeric values that represent the access permissions for each set.

0 = -

4 = r--

5 = r-x

6 = rw- 

7 = rwx

[ Reference: permissions calculator ](http://permissions-calculator.org/)


Set permissions for a file

    chmod <octal number> <filename>
eg.

    chmod 744 my_first_script.sh

# Systems Path
The systems path is a variable `($PATH)`. It references a list of directories that should be known to the shell so that when a filename is written in the shell as a command, the shell knows within which folders to search for executable files.

A directory can be added to the path variable by amending the .zshrc file in the users root folder:

    export PATH=“$PATH:$HOME/bash_course/scripts”

[ How to add to the shell path using macOS ]((https://wpbeaches.com/how-to-add-to-the-shell-path-in-macos-using-terminal/))