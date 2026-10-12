# Bandit Level 0 → Level 1

## Objective
Find the password for Level 1 by exploring the Bandit server through the Linux terminal.

## Concepts Learned
- SSH (Secure Shell)
- Linux file navigation
- Listing files using `ls`
- Reading files using `cat`

## Steps Performed

### 1. Connected to the Bandit server

Used SSH to connect to the server as `bandit0` on port `2220`.

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

### 2. Listed the files

```bash
ls
```

The `ls` command displays files and directories in the current directory. It helped me locate the `readme` file.

### 3. Read the password file

```bash
cat readme
```

The `cat` command displays the contents of a file. The output contained the password needed for the next level.

### 4. Logged in as bandit1

Used the retrieved password to authenticate to the server as `bandit1`.

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

<img width="199" height="54" alt="image" src="https://github.com/user-attachments/assets/ecba1d9d-e9d6-43ee-8ba4-bfd8ee16e364" />


## Key Takeaways
- SSH provides secure remote access to a system.
- `ls` helps identify files in a directory.
- `cat` can display the contents of a text file.
- Different user accounts can provide access to different stages of a security exercise.

## Security Note
Passwords and credentials have been excluded from this write-up.
