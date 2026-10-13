# Bandit Level 2 → Level 3

## Objective
Retrieve the password for Level 3 from a file whose name contains spaces and hyphens.

## Step 1: Log in as bandit2

Used SSH to connect to the Bandit server with the password obtained from the previous level.

```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

- `ssh` establishes a secure remote connection.
- `bandit2` is the username.
- `bandit.labs.overthewire.org` is the server hostname.
- `-p 2220` specifies the SSH port.

## Step 2: List the files

```bash
ls
```

The command listed the files in the current directory. One file was named:

`--spaces in this filename--`

The filename contains spaces and hyphens.

## Step 3: Read the file

```bash
cat "./--spaces in this filename--"
```

The command displayed the file contents, which contained the password for the next level.

## Understanding the Command

- `cat` displays a file's contents.
- `./` specifies a path relative to the current directory.
- Double quotes keep the spaces in the filename together as one argument.
- The hyphens are part of the filename.

## Key Takeaways
- SSH allows secure access to remote systems.
- `ls` lists files and directories.
- Quoting filenames helps the shell handle spaces correctly.
- Using `./` explicitly identifies a file in the current directory.

## Security Note
Passwords and credentials have been excluded from this write-up.
