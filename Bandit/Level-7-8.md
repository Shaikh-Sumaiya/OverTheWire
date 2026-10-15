# Bandit Level 7 → Level 8

## Objective

Find the password for the next level in the file `data.txt`. The password is on the line containing the word `millionth`.

## Step 1: Log in as bandit7

Connect to the Bandit server using SSH:

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

## Step 2: Open the file using less

```bash
less data.txt
```

The file contained a large amount of text, so I used `less` to navigate through it instead of displaying everything at once with `cat`.

## Step 3: Search for the keyword

While inside `less`, I entered:

```text
/millionth
```

**Explanation:**

- `/` starts a forward search in `less`.
- `millionth` is the keyword being searched for.
- Pressing `Enter` takes you to the matching result.
- Press `n` to find the next match and `q` to exit `less`.

The matching line contained the password for the next level.

## Alternative Method: Using grep

The same result can be found directly using `grep`:

```bash
grep "millionth" data.txt
```

**Explanation:**

- `grep` searches text for a specified pattern.
- `"millionth"` is the keyword being searched for.
- `data.txt` is the file being searched.

This command displays the line containing `millionth` without opening the file interactively.

## Key Takeaways

- Use `less` to navigate large text files without flooding the terminal.
- Search within `less` using `/keyword`.
- Press `n` to move to the next match and `q` to quit.
- Use `grep` to find matching lines directly in a file.

## Security Note

Never include passwords or other sensitive credentials in public GitHub write-ups.
