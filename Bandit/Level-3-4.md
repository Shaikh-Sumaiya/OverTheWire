# Bandit Level 3 → Level 4

## Objective
Find the password for the next level in a hidden file inside the `inhere` directory.

## Step 1: Log in as bandit3

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

Used the password obtained from the previous level to connect to the Bandit server as `bandit3`.

## Step 2: List the directory

```bash
ls
```

The output showed a directory named `inhere`.

## Step 3: Enter the directory

```bash
cd inhere
```

The `cd` command changes the current working directory.

## Step 4: Display hidden files

```bash
ls -a
```

The `-a` option displays all directory entries, including hidden files whose names begin with a dot (`.`).

## Step 5: Read the hidden file

Used `cat` with the hidden filename to display its contents and retrieve the password for the next level.

## Key Takeaways
- `cd` changes the current directory.
- `ls` lists visible files and directories.
- `ls -a` also displays hidden files.
- On Linux, filenames beginning with a dot are hidden by convention.

## Security Note
Passwords and credentials have been excluded from this write-up.
