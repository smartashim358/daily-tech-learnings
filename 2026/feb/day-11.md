# Linux File System Learning Status

## Overview

Today's learning focused on understanding the Linux file system at a
deeper level.\
The goal was to move beyond basic commands and understand how Linux
actually manages files internally.

This document summarizes the concepts, definitions, examples, and
commands covered.

------------------------------------------------------------------------

# 1. Home Directory (`~`)

## Definition

The tilde symbol `~` represents the current user's **home directory**.

For example: If the username is `kali`, then:

    ~  →  /home/kali

## Why It Is Used

-   Shortens long paths
-   Makes commands portable between users
-   Improves efficiency

## Example

``` bash
cd ~
mkdir ~/fs_lab
```

------------------------------------------------------------------------

# 2. Removing Non-Empty Directories

## Definition

By default, Linux does not remove directories that contain files.

## Commands

Remove empty directory:

``` bash
rmdir foldername
```

Remove non-empty directory:

``` bash
rm -r foldername
```

Force remove (dangerous):

``` bash
rm -rf foldername
```

Safe interactive removal:

``` bash
rm -ri foldername
```

------------------------------------------------------------------------

# 3. Moving and Copying Files

## Move File

``` bash
mv file.txt /path/to/destination/
```

## Rename File

``` bash
mv old.txt new.txt
```

## Copy File

``` bash
cp file.txt backup/
```

## Copy Folder Recursively

``` bash
cp -r folder1 backup/
```

## Preserve Permissions & Metadata

``` bash
cp -a folder1 backup/
```

------------------------------------------------------------------------

# 4. Finding Files

## Find by Name

``` bash
find . -name "file.txt"
```

## Case-Insensitive Search

``` bash
find . -iname "file.txt"
```

## Find by Extension

``` bash
find . -name "*.log"
```

## Find by Size

``` bash
find . -size +10M
```

------------------------------------------------------------------------

# 5. Searching Keywords Inside Files (grep)

## Basic Search

``` bash
grep "error" file.txt
```

## Recursive Search

``` bash
grep -r "error" .
```

## Show Line Numbers

``` bash
grep -rn "error" .
```

## Case-Insensitive Recursive Search

``` bash
grep -ri "error" .
```

------------------------------------------------------------------------

# 6. Hard Links

## Definition

A hard link is another filename that points to the same inode (same file
data).

## Create Hard Link

``` bash
ln original.txt hardlink.txt
```

## Key Properties

-   Same inode number
-   No extra disk space used
-   Survives deletion of original file
-   Cannot cross filesystems
-   Cannot link directories (normally)

## Example

``` bash
echo "hello" > file1.txt
ln file1.txt file2.txt
ls -li
```

If one file is deleted:

``` bash
rm file1.txt
```

`file2.txt` still works.

------------------------------------------------------------------------

# 7. Soft Links (Symbolic Links)

## Definition

A soft link is a shortcut that points to a file path.

## Create Soft Link

``` bash
ln -s original.txt softlink.txt
```

## Key Properties

-   Different inode
-   Can link directories
-   Can cross filesystems
-   Breaks if original file is deleted

------------------------------------------------------------------------

# 8. Checking File Information

## View File Metadata

``` bash
stat file.txt
```

## View Disk Usage

``` bash
du -sh *
df -h
```

------------------------------------------------------------------------

# 9. File Permissions

## Change Permissions (Numeric)

``` bash
chmod 755 file.sh
```

## Change Permissions (Symbolic)

``` bash
chmod u+x file.sh
```

## Change Ownership

``` bash
sudo chown user:group file.txt
```

------------------------------------------------------------------------

# 10. Compression and Archiving

## Create Archive

``` bash
tar -cvf backup.tar folder1/
```

## Extract Archive

``` bash
tar -xvf backup.tar
```

## Compressed Archive

``` bash
tar -czvf backup.tar.gz folder1/
```

------------------------------------------------------------------------

# Key Takeaways

-   Linux files are based on inodes.
-   Hard links share the same inode.
-   Soft links point to file paths.
-   `find` and `grep` are essential for file discovery.
-   Proper use of `rm -r` and `chmod` is critical for system control.
-   Understanding file structure is foundational for cybersecurity and
    backend systems.

------------------------------------------------------------------------

# Learning Outcome

After this session, the learner can:

-   Navigate and manipulate the Linux file system confidently.
-   Remove, move, copy, and search files effectively.
-   Understand and use hard and soft links properly.
-   Analyze file metadata and permissions.
-   Apply these concepts in cybersecurity and backend development
    contexts.

------------------------------------------------------------------------

End of Report
