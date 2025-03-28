# Init, clone
`git init` can be used to convert an existing, unversioned project to a Git repository or initialize a new, empty repository

`git clone` is used to pull the entire project to the current working directory. It can be done with **https** or **ssh-key** protocol

To uninitialize the project simply remove `.git` directory from the folder where `git init` or `git clone` was called
# Handling staging area and managing commits
In the working directory files can be moved to staging area with `git add <file>` command

`git reset` can be used to reset changes in repository to a specific commit, unstage changes in the staging area, or remove commits entirely
`git reset <file>` unstages changes to a file in the staging area, leaving the changes in the working directory
`git reset [--soft|--mixed|--hard] <commit>` resets the repository to the specified commit and
`--soft` preserving changes in the working directory and the staging area
`--mixed` leaving changes in the working direcotry but removing them from the staging area
`--hard` discarding any changes in the working directory and the staging area

`git commit` is used to save changes to the Git repository. It records the changes have been made in local repository. Serves as a snapshot of code, allowing to revert to previous version of code

`git push` is used to upload local repository content to a remote repository. It is the way of transfering  commits from local repository to remote repo
By default the command is `git push [remote repo] [local brach]` - In case of tracking braches the two switches can be left

`git pull` is used to fetch and download content from a remote repository and immediately update the local repository to match that content
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTczOTExNzE0NV19
-->