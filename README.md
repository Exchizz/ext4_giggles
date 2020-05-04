# What is this ?
I'm just playing around with understanding ext4 and how it allocates files

## How do I compile this ?
```
 gcc main.c
```

## How do I test this ?
### 1. Create an empty file
```
dd if=/dev/zero bs=1M count=512 of=fs_ext4.img
```
### 2. Create an ext4 filesystem in the file from step 1
```
mkfs.ext4 fs_ext4.img
```

### 3. Mount the newly created ext4 filesystem
```
sudo mount fs_ext4.img mp
```
Where mp is a directory.


By creating, deleting etc. files in the mp/ filesystem, you can see the changes made tot he filesystem using the code in main.c

# Example:
### 1. Create file with content "Hello world" in newly created filesystem
```
echo "Hello world" > mp/file1
```

### 2. Print inode of newly created file
```
ls -li mp/
```

In my case the inode is 12 (left most column)

### 3. Use main.c to dig in the filesystem to see where the data of inode to is resting on the filesystem.
(remember to change 11 on line 334 if your inode is not 12)
```
./a.out
```

### 4. Read file form filesystem using dd
Look for line starting with "index: 5, data: " - it will show the byte cound to where the data of the file is located.
In my case, it's 33792 bytes into the file

```
dd if=fs_ext4.img bs=4096 skip=33792 count=1 status=none | xxd -s 0 -l 12 -b
```

dd will then print the output of the file and converted into ascii by xxd
