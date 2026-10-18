# Bandit Level 12 → Level 13

## Objective

The password for the next level is stored in `data.txt`. The file contains a hexdump of a file that has been repeatedly compressed.

The goal is to reverse the hexdump, identify each file format, and decompress or extract the file repeatedly until the password is revealed.

## Step 1: Log in as bandit12

Connect to the Bandit server using SSH:

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

## Step 2: Create a temporary working directory

The challenge recommends working inside `/tmp` so that the original file remains untouched.

```bash
mktemp -d
```

This creates a temporary directory with a randomly generated name, such as `/tmp/tmp.XXXXXXXXXX`.

Copy the file into the new directory, move into it, and rename the copy:

```bash
cp data.txt /tmp/your-directory-name/
cd /tmp/your-directory-name
mv data.txt data
```

Replace `/tmp/your-directory-name/` with the actual path printed by `mktemp -d`.

**Why these commands?**

- `mktemp -d` creates a temporary directory with a unique name.
- `cp` copies the original file into the working directory.
- `cd` changes the current directory.
- `mv` renames the copied file from `data.txt` to `data`.

Keeping a separate working copy lets us transform the file without modifying the original.

## Step 3: Reverse the hexdump

The file named `data` is a hexdump, which represents binary data as readable hexadecimal text.

```bash
xxd -r data > decoded
```

**Command breakdown:**

- `xxd` displays file data in hexadecimal format.
- `-r` reverses a hexdump back into binary data.
- `data` is the input file.
- `>` redirects the output into a new file named `decoded`.

Identify the reconstructed file:

```bash
file decoded
```

Output:

```text
decoded: gzip compressed data
```

This tells us that the reconstructed file is compressed using GZIP.

## Step 4: Decompress the first GZIP layer

Rename the file to use the `.gz` extension, then decompress it:

```bash
mv decoded data2.gz
gunzip data2.gz
```

The output is a file named `data2`.

Check its format:

```bash
file data2
```

Output:

```text
data2: bzip2 compressed data
```

The first GZIP layer has been removed, revealing a bzip2-compressed file.

## Step 5: Decompress the bzip2 layer

Run:

```bash
bunzip2 data2
```

Because `data2` does not have the usual `.bz2` extension, the command reports:

```text
bunzip2: Can't guess original name for data2 -- using data2.out
```

This is not a failure. The file is decompressed, and the output is saved as `data2.out`.

Identify the next layer:

```bash
file data2.out
```

Output:

```text
data2.out: gzip compressed data
```

The next layer is GZIP again.

## Step 6: Decompress the second GZIP layer

Rename the file and decompress it:

```bash
mv data2.out data3.gz
gunzip data3.gz
```

Check the resulting file:

```bash
file data3
```

Output:

```text
data3: POSIX tar archive (GNU)
```

This time, the file is a TAR archive rather than another compressed stream.

## Step 7: Extract the first TAR archive

Use `tar` to extract the archive:

```bash
tar -xf data3
```

**Command breakdown:**

- `tar` works with TAR archives.
- `-x` extracts the archive contents.
- `-f` specifies the archive filename.
- `data3` is the archive being extracted.

List the files:

```bash
ls
```

A new file named `data5.bin` appears.

Identify it:

```bash
file data5.bin
```

Output:

```text
data5.bin: POSIX tar archive (GNU)
```

The extracted file is another TAR archive.

## Step 8: Extract the second TAR archive

Run:

```bash
tar -xf data5.bin
```

List the files again:

```bash
ls
```

The next file is `data6.bin`.

Identify its format:

```bash
file data6.bin
```

Output:

```text
data6.bin: bzip2 compressed data
```

We have reached another bzip2-compressed file.

## Step 9: Decompress the next bzip2 layer

Rename the file to use the expected extension and decompress it:

```bash
mv data6.bin data6.bz2
bunzip2 data6.bz2
```

The resulting file is named `data6`.

Check its format:

```bash
file data6
```

Output:

```text
data6: POSIX tar archive (GNU)
```

Another TAR archive is waiting to be extracted.

## Step 10: Extract the third TAR archive

Run:

```bash
tar -xf data6
```

List the files:

```bash
ls
```

The next file is `data8.bin`.

Identify it:

```bash
file data8.bin
```

Output:

```text
data8.bin: gzip compressed data
```

We have reached another GZIP layer.

## Step 11: Decompress the final GZIP layer

Rename the file and decompress it:

```bash
mv data8.bin data8.gz
gunzip data8.gz
```

Now identify the resulting file:

```bash
file data8
```

Output:

```text
data8: ASCII text
```

The file is now ordinary readable text rather than another compressed archive.

## Step 12: Read the password

Display the final file:

```bash
cat data8
```

The output contains the password for `bandit13`.

**Security reminder:** Never include the actual password in this writeup or commit it to GitHub.

## Compression Layers: Quick Reference

| Stage | File | Detected format | Command used |
|---|---|---|---|
| 1 | `data` | Hexdump | `xxd -r data > decoded` |
| 2 | `decoded` | GZIP | `gunzip data2.gz` |
| 3 | `data2` | bzip2 | `bunzip2 data2` |
| 4 | `data2.out` | GZIP | `gunzip data3.gz` |
| 5 | `data3` | TAR | `tar -xf data3` |
| 6 | `data5.bin` | TAR | `tar -xf data5.bin` |
| 7 | `data6.bin` | bzip2 | `bunzip2 data6.bz2` |
| 8 | `data6` | TAR | `tar -xf data6` |
| 9 | `data8.bin` | GZIP | `gunzip data8.gz` |
| 10 | `data8` | ASCII text | `cat data8` |

The filenames in the command column reflect the renaming steps performed before decompression where necessary.

## Key Takeaways

### 1. Identify files before processing them

```bash
file filename
```

The `file` command examines a file's contents and helps identify its format. This is especially useful when the filename or extension does not reveal what it contains.

### 2. Know which tool to use

| Tool | Purpose |
|---|---|
| `xxd -r` | Reconstruct binary data from a hexdump |
| `gunzip` | Decompress GZIP files |
| `bunzip2` | Decompress bzip2 files |
| `tar -xf` | Extract TAR archives |
| `mv` | Rename or move files |
| `cp` | Copy files |
| `ls` | List directory contents |
| `cat` | Display file contents |
| `file` | Identify file types |

### 3. Understand compression versus archiving

- **GZIP and bzip2** compress data.
- **TAR** packages files into an archive; creating a TAR archive does not necessarily compress its contents.
- A file may contain a compressed stream or archive inside another compressed stream or archive.

### 4. Work with temporary directories

Using `mktemp -d` provides an isolated workspace for experiments and keeps the original challenge file unchanged.

### 5. Do not rely on file extensions alone

A file named `data6.bin` can still be a bzip2 stream, and a file named `data3` can be a TAR archive. Use `file` to identify the actual format instead of guessing from the name.

## Conclusion

Bandit Level 12 → Level 13 involved reversing a hexdump and working through multiple layers of GZIP, bzip2, and TAR formats. The most important lesson was to identify each layer using `file`, apply the appropriate tool, and repeat the process until readable text was recovered.


<img width="1312" height="1199" alt="image" src="https://github.com/user-attachments/assets/3ac14e36-80a2-4018-8c18-bb5f963a67b0" />
