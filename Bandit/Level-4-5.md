# Bandit Level 4 → Level 5

## Objective
Find the password for the next level in the only human-readable file inside the `inhere` directory.

## Step 1: Log in as bandit4

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

Used the password obtained from the previous level to connect to the Bandit server as `bandit4`.

## Step 2: List the files

```bash
ls
```

The output showed the `inhere` directory.

## Step 3: Enter the directory

```bash
cd inhere
```

The `cd` command changes the current working directory.

## Step 4: List the files inside

```bash
ls
```

The directory contained 10 files.

## Step 5: Identify the human-readable file

Used the `cat` command to inspect the files and found that `-file07` contained human-readable text.

```bash
cat ./-file07
```

The output contained the password for the next level.

## Key Takeaways
- `cd` is used to navigate between directories.
- `ls` lists files and directories.
- `./` specifies a file in the current directory.
- The `cat` command displays file contents.

## Security Note
The password has been excluded from this write-up.
