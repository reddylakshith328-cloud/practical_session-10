# Practical Session 10

## Investigating Inodes, Hard Links and Symbolic Links in Linux

### Aim

To investigate Linux inode structures using `ls -i`, `ls -li`, `stat`, and `find`, and understand the behavior of hard links and symbolic links.

### Experiments

#### 1. Inode Investigation
- Created `original.txt`
- Examined inode information using `ls -i` and `stat`
- Observed inode number, permissions, size, timestamps, and link count

#### 2. Hard Links
- Created `hardlink.txt`
- Verified that `original.txt` and `hardlink.txt` share the same inode
- Modified the file through the hard link
- Deleted the original filename and verified that the hard link still works

#### 3. Symbolic Links
- Created `symlink.txt`
- Verified that the symbolic link has its own inode
- Used `stat`, `stat -L`, and `readlink`
- Demonstrated a broken symbolic link

#### 4. Find Commands
Used:
- `find . -inum`
- `find . -type l`
- `find . -type l -ls`

#### 5. mmap() File I/O
Implemented file modification using:
- `mmap()`
- `msync()`
- `munmap()`

#### 6. read()/write() File I/O
Implemented the same file modification using:
- `read()`
- `lseek()`
- `write()`

### Performance Comparison

Measured execution time:

| Method | Real Time |
|---|---:|
| mmap() | 0.003 s |
| read()/write() | 0.002 s |

The experiment showed that both methods successfully modified the file. In this particular run, `read()/write()` was slightly faster.

### Source Files

- `mmap_file.c`
- `read_write_file.c`
- `inode_lab/`

### Compilation

```bash
gcc -Wall -Wextra -g mmap_file.c -o mmap_file
gcc -Wall -Wextra -g read_write_file.c -o read_write_file
