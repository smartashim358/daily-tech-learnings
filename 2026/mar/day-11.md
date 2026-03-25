# Linux File System Commands - Structured Notes

## 1. Navigation Commands

### pwd
Shows current directory
```
pwd
```

### ls
List files and directories
```
ls
ls -l
ls -a
ls -lh
```

### cd
Change directory
```
cd /path
cd ..
cd ~
cd -
```

---

## 2. File & Directory Management

### Create Files
```
touch file.txt
```

### Create Directories
```
mkdir folder
mkdir -p a/b/c
```

### Delete
```
rm file.txt
rm -r folder
rm -rf folder
```

### Copy
```
cp file.txt backup.txt
cp -r folder1 folder2
```

### Move / Rename
```
mv file.txt newname.txt
mv file.txt /path
```

---

## 3. File Viewing

### cat
```
cat file.txt
```

### less
```
less file.txt
```

### head / tail
```
head file.txt
tail file.txt
tail -f log.txt
```

---

## 4. File Editing

### nano
```
nano file.txt
```

### vim
```
vim file.txt
```

---

## 5. Permissions & Ownership

### chmod
```
chmod 755 file.txt
chmod +x script.sh
```

### chown
```
chown user:group file.txt
```

---

## 6. Search Commands

### find
```
find /home -name file.txt
find . -type f
```

### locate
```
locate file.txt
```

---

## 7. Disk Usage

### df
```
df -h
```

### du
```
du -sh folder
```

---

## 8. Links

### Hard Link
```
ln file.txt hardlink
```

### Soft Link
```
ln -s file.txt softlink
```

---

## 9. Important Directories

- / : root
- /home : user files
- /etc : config
- /var : logs
- /bin : system commands
- /usr : applications

---

## 10. Advanced Commands

### mount / umount
```
mount /dev/sdb1 /mnt
umount /mnt
```

### stat
```
stat file.txt
```

### file
```
file file.txt
```

### chattr
```
chattr +i file.txt
```

### lsof
```
lsof | grep file.txt
```

---

## 11. Pro Commands

### inode usage
```
df -i
```

### filesystem check
```
fsck /dev/sda1
```

### backup
```
rsync -av folder/ backup/
```

---

## 12. Quick Learning Tips

- Master navigation first
- Practice file operations daily
- Understand permissions deeply
- Use find and disk tools regularly
- Move to advanced after basics

---

## End of Notes
