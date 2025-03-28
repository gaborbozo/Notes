# Common commands
## Information and navigation
### uname
`uname -a`
### pwd
Current working directory
### cd
`cd -` for previous directory
### ls
`ls -R` for subdirectories
`ls -a` for hidden files
`ls -l` for detailed informations
## File handling
### cat
Used to list the contents of a file on the standard output
`cat > file1` create a new file
`cat file1 > file2` copy `file1`'s data to `file2`
`cat file1 file2 > file3`
### echo
 Displaying lines of text or string which are passed as arguments on the command line
### cp
 Copies a file to a specific directory
### mv
Moves files, although it can also be used to rename files
### locate
Locate a file
`locate -i file` for case sensitivity
`locate green*apple` for files that contains green and apple
### find
Locate a file or a directory in a given path
`find . -type f -name file`
`find . -type d -name directory`
### which
Locate a command by searching the command executable in the directories specified by the environmental variable PATH
## Data analysis
### grep
Searches for a given keyword
`grep keyword input`
### head
View the first lines of any text file
### tail
View the last lines of any text file
### diff
Compares the contents of two files line by line, then it will output the lines that do not match
## Data formatting
### tar
Common Linux file format that is similar to `.zip` format, with compression being optional
### zip
## Permissions
### chmod
### chown
Enables to transfer the ownership of a file to a specific user
## Processes
## ps
Produces a snapshot of all running processes
### top/htop
Resource-hungry processes first
### atop
Monitoring system resources. Once it is launched, atop will show the resource usage for the CPU, memory, swap, disks, and network in 10-second intervals
### jobs

## Internet
### hostname
`hostname -i`
### ping
Checks connectivity status to a server
### wget
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MzMzNzIzOTFdfQ==
-->