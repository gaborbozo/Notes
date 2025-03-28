Distributed Version Control system

Git commits requires names and emails
```git
git config --global user.name "user_name"
git config --global user.email "user_emaik"
```

A **snapshot** is a representation of the current state of tracked files in the form of a manifest, which can be compared with other manifests to see where the differences are
Git only tracks the differences between manifests **from the first moment it was tracked**

![](https://lh3.googleusercontent.com/QDDTje49GwcDBC_TRTntEcA3AGTDID1-rD4Z_uGAhphTulmXl6Fc-RkkPcfr39zlBp2QldbgHbd8kOEl8_EMvM3Itt5TQLw8XkbafL-U2RE27zuvovUSOWia6etUmUZ9tPzY0dRGa1r5wl4XkbI-FBSISMWidCSk0wpNMlwMr-Zs30ZhgjUHfx5vC77yu50TKvQBgrZ25HRXtM-7j-h5da9wRn2sXKsmw5rrM75KXrz0eIH0hrdWAsD5-I-N0AnvKqXrcfF1du4qqZClC4zofByZwJlr_t2Gb3xcqBhTlVi-FFEhXem11hvc8l2ufE8xvsJwMRbgIHcGk2IAnjdDV5LprBLGhQe6BlsiLw0M8OkOzBI47esfWWPcH6tR4gGW50OJlC8oDfd0syXYn5n9wCwGO9ldc8Unb0ggd4rfi18STPWFxUTWVFQ_NiFY6IwNV78wdvGhiAur0gb4dV3fVASsleYST1UZ8pcESSp4hjKOVFF61F1NlP1Z0NxwwEKR_qU1uNMBTr_VDPCV3_3eTg0BLmdddAkkKENwRNVf3nAGO6esF8cgFp5apIFWokBGmhTnJEwwaRkUp-t66JG_yVYEm-bhaf_yq_kyQv2LXJfhUwUwoWQ9oM-Fi8i8dkx7Ofzd64nzUp1TFFE_yQPJrSsAFPXvLMH47hT-bwN__38XJB-ZxCcEK0kdVBBHH41oZCeP5pOuOB-hBLfVWsyFcjicLtJMltQIUav6RoRD_VHi23xiLYB9uCzpcHEHKVEIqHF6HEB09kHoyFhuIepZ4NsMbDGNZGlRKTin0QGpgE0DhIdFY5icV4DpyvwUyy2qzb-62XZTSOh4yy5p7Brcr4qsEle7hip-NzadgNOHjHLwn8BTEjJeuzV9BTWVd81foIBqoahIkI44KEGvRJmnScq22TlVe8IciE2sMH9WY_XZh9xD=w768-h720-no?authuser=0)
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
eyJoaXN0b3J5IjpbMTE0OTgyMzI0XX0=
-->