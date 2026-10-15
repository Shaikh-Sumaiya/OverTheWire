# Bandit Level 6 → Level 7

## Objective

Find a file somewhere on the server that meets these conditions:

- Owned by user `bandit7`
- Owned by group `bandit6`
- Exactly 33 bytes in size

## Step 1: Log in as bandit6

Connect to the Bandit server using SSH:

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

## Step 2: Search for the file

The `ls` command did not show any files in the current directory. Since the target file could be anywhere on the server, I used `find` to search from the root directory.

```bash
find / -type f -user bandit7 -group bandit6 -size 33c
```

**Explanation:**

- `/` searches from the root directory.
- `-type f` searches for regular files only.
- `-user bandit7` matches files owned by user `bandit7`.
- `-group bandit6` matches files belonging to group `bandit6`.
- `-size 33c` matches files exactly 33 bytes in size.

## Step 3: Hide permission errors

To make the output easier to read, I used:

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

**Explanation:**

- `2` represents standard error (stderr).
- `>` redirects the error output.
- `/dev/null` discards anything sent to it.

This hides error messages, such as `Permission denied`, while keeping matching file paths visible. It does not change the search or bypass file permissions.

## Step 4: Read the file

After identifying the matching file, I used `cat` with the returned file path to read its contents and retrieve the password for the next level.

## Key Takeaways

- Use `find /` to search across the filesystem.
- Combine `-user`, `-group`, and `-size` to narrow down search results.
- Use the `c` suffix to specify file size in bytes.
- Use `2>/dev/null` to hide error messages without affecting the search.
- Use `cat` to read a file's contents.

## Security Note

Never publish passwords or other sensitive credentials in public GitHub repositories.
