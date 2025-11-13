Distributed Version Control system

Git commits requires names and emails
```git
git config --global user.name "user_name"
git config --global user.email "user_emaik"
```

A **snapshot** is a representation of the current state of tracked files in the form of a manifest, which can be compared with other manifests to see where the differences are
Git only tracks the differences between manifests **from the first moment it was tracked**

![](https://lh3.googleusercontent.com/d/12NTUwpUC1MN1EQOXBdUT0isZH3QQ0Z6e)
# Remote repository
Central source of "truth" for a team of developers to collaborate on a project
Developers push their snapshots to here(in form of commit) and pulls updates from it
A remote servers hosts it, for example github, gitlab, bitbucket and etc
# Local repository
Acts like the remote repository but in local
Contains a complete history of all the changes made to the project and allows the developer to work on the project without an internet connection
Can be synchronized with a remote repository, allowing the developer to share changes with other collaborators and stay up-to-date
# Staging area
An intermediate storage area where changes made to the local repository can be reviewed and prepared for commit
Allows developers to stage individual changes, or chunks of changes, before committing them to the local repository
This functionality allows for more granular control over what gets committed, and makes it easier to craft meaningful, well-organized commits
# Working directory
Live version of the project
Changes made to the files in the working directory are not tracked by Git until they are staged and committed
Represents the state of the project at a given point in time
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkxNzA0MjkwNiwxMTQ5ODIzMjRdfQ==
-->