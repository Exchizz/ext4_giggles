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
