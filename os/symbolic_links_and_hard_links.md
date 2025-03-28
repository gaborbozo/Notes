# Symbolic links
Symbolic links/soft links are pointers that can point either to a target file or a directory
The symbolic link is a second file that exists independently of its target
If a symbolic link points to a target, and sometime later that target is moved(dangling), renamed(broken/orphaned) or deleted(dead), the symbolic link is not automatically updated or deleted, but continues to exist and still points to the old target, now a non-existing location or file
If a symbolic link is deleted, its target remains unaffected
Symbolic links may point to any file or directory irrespective of the volumes on which the link and target reside
# Hard links
Hard link is a directory entry (in a directory-based file system) that associates a name with a file
Each file must have atleast one hard link
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MTM4NDk4NTBdfQ==
-->