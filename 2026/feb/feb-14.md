# Linux Permissions & Special Bits --- Quick Recall Notes

## 1. Basic File Permissions

### Definition

Linux permissions control who can read, write, or execute a file. They
are divided into three classes: Owner, Group, and Others.

### Permission Values

-   4 = Read (r)
-   2 = Write (w)
-   1 = Execute (x)

### Examples

-   7 = 4+2+1 = rwx
-   6 = 4+2 = rw-
-   5 = 4+1 = r-x

Example: chmod 755 file Owner = rwx Group = r-x Others = r-x

------------------------------------------------------------------------

## 2. Directory Permissions (Different Logic)

### Definition

Directory permissions control access to the directory structure, not
file content.

Permission meanings for directories: - r = List filenames (ls) - w =
Create/Delete/Rename files - x = Enter directory (cd) and access items

### Key Rule

To delete a file, you need write + execute on the directory, not on the
file itself.

------------------------------------------------------------------------

## 3. Execute vs Read in Scripts

### Definition

Scripts require both read and execute permissions because the shell must
read the script before executing it.

-   --x only → Cannot run script
-   r-x → Script runs successfully

Binary programs only require execute permission.

------------------------------------------------------------------------

## 4. umask (Default Permission Policy)

### Definition

umask defines which permissions are removed from default permissions
when new files or directories are created.

### Default Base Values

-   Files start at 666
-   Directories start at 777

### Example

If: umask 022

Then: - File: 666 - 022 = 644 - Directory: 777 - 022 = 755

umask 077 → creates private files (600) and directories (700).

------------------------------------------------------------------------

## 5. Special Permission Bits (4th Digit)

When using four digits in chmod, the first digit controls special bits.

-   4 = setuid
-   2 = setgid
-   1 = sticky bit

Example: chmod 4755 program

Breakdown: - 4 = setuid - 755 = normal permissions

------------------------------------------------------------------------

## 6. setuid

### Definition

When enabled on a file, the program runs with the owner's privileges
instead of the user's.

### Use Case

System tools that need temporary elevated privileges.

------------------------------------------------------------------------

## 7. setgid

### Definition

On files: Program runs with the file's group privileges. On directories:
New files inherit the directory's group.

### Use Case

Team collaboration directories to maintain consistent group ownership.

------------------------------------------------------------------------

## 8. Sticky Bit

### Definition

When set on a directory, users can delete only their own files inside
it.

### Use Case

Used in shared directories to prevent users from deleting others' files.

------------------------------------------------------------------------

## 9. Core Concepts to Remember

-   File permissions control data access.
-   Directory permissions control structure access.
-   Execute on directory = ability to enter.
-   Deletion depends on directory permissions.
-   umask subtracts from default permissions.
-   Special bits modify execution behavior.

------------------------------------------------------------------------

## Quick Learn

Files → Control data Directories → Control namespace umask → Default
policy Special bits → Privilege behavior modifier

------------------------------------------------------------------------

End of Notes.
