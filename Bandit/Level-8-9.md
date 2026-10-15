# Bandit Level 8 → Level 9

## Objective

Find the password for the next level in `data.txt`. The password is the only line of text that occurs exactly once.

## Step 1: Log in as bandit8

Connect to the Bandit server using SSH:

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

## Step 2: Sort the file and remove duplicate lines

My initial command was:

```bash
sort data.txt | uniq
```

**Explanation:**

- `sort data.txt` sorts the lines alphabetically.
- `|` (pipe) passes the output of one command to another.
- `uniq` removes consecutive duplicate lines, keeping one copy of each repeated line.

This removes duplicate occurrences but still displays lines that appeared multiple times.

## Step 3: Display only unique lines

I modified the command by adding the `-u` option:

```bash
sort data.txt | uniq -u
```

**Explanation:**

- `sort` groups identical lines together.
- `uniq -u` displays only lines that occur exactly once.

The output revealed the password for the next level.

## Alternative: Count line occurrences

```bash
sort data.txt | uniq -c
```

The `-c` option displays each line alongside the number of times it occurs. This is useful for understanding how frequently lines appear.

## Key Takeaways

- `sort` arranges lines so identical entries appear together.
- `uniq` removes consecutive duplicate lines.
- `uniq -u` displays lines that occur exactly once.
- `uniq -c` counts occurrences of each line.
- Pipes (`|`) allow commands to work together.

## Security Note

Never include passwords or other sensitive credentials in public GitHub write-ups.
