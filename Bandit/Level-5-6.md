# Bandit Level 5 → Level 6

## Objective

Find the file inside the `inhere` directory that meets the following conditions:

- Human-readable
- Exactly 1033 bytes in size
- Not executable

## Step 1: Log in as bandit5

Connect to the Bandit server using SSH:

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

## Step 2: Navigate to the inhere directory

```bash
cd inhere
```

The directory contained multiple subdirectories, making it inefficient to check every file manually.

## Step 3: Find the file by size

```bash
find . -type f -size 1033c
```

**Explanation:**
- `find` searches for files and directories.
- `.` searches recursively from the current directory.
- `-type f` searches for regular files only.
- `-size 1033c` matches files exactly 1033 bytes in size. The `c` suffix specifies bytes.

## Step 4: Exclude executable files

```bash
find . -type f -size 1033c ! -executable
```

**Explanation:**
- `! -executable` excludes files executable by the current user.
- Combining conditions narrows the search to files matching the challenge requirements.

The command identified the target file. Reading its contents revealed the password for the next level.

## Key Takeaways

- Use `find` to search recursively through nested directories.
- Use `-type f` to search for regular files.
- Use `-size Nc` to match an exact file size in bytes.
- Use `! -executable` to exclude executable files.
- Combining search conditions is faster than manually checking every file.

## Security Note

Passwords and other sensitive credentials should never be included in public GitHub write-ups.
