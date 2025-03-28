`.gitignore` file lets Git know that it should ignore certain files and not track them when `git add` command was called, files like private keys, log files, generated files and etc

Plain text file where each line contains a pattern for files/directories to ignore
Generally placed in the root folder of the repository however, can be put it in any folder in the repository and can also have multiple `.gitignore` files at the same time
# Literal files
`file_name` will ignore all the files named as `file_name`
# Path
`directory/` will ignore the entire directory of adding it to the tree
# Wildcards
## Asterisk
`*` matches zero or more characters except `/` 

`*.log`
## One character
`?` matces one character except `/`

`???.log` ignores all `.log` files having exactly 3 characters intheir name
## Double Asterisk
`**` matches any number of directories

`**/deep_nested_file`
`**/deep-nested-directory`
`**/logs/*.log`  matches all files ending with  `.log`  in a logs directory
`logs/**/*.log`  matches all files ending with  `.log`  in the logs directory and any of its subdirectories
`logs/**` matches all files inside of logs
# Negate
`!` prefix negates a file that would be ignored

`*.log`
`!important.log`
Negates all log files, except `important.log`

Negating a file in an ignored folder in Git by adding a negation pattern to `.gitignore` may not always work
If the directory containing the file is ignored by a higher-level `.gitignore` or if the file has already been added to Git's internal list of ignored files, the negation will not take effect
To start tracking such a file, use `git rm --cached` to remove it from Git's internal list of ignored files, then add and commit it
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUzODc2NzA3MV19
-->