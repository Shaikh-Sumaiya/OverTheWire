# Bandit Level 9 → Level 10

## Objective

Find the password in `data.txt`. It is stored in one of the human-readable strings preceded by several `=` characters.

## Step 1: Log in as bandit9

Connect to the Bandit server using SSH:

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

## Step 2: Extract human-readable strings

```bash
strings data.txt
```

The file contained non-text data, so I used `strings` to extract readable text. Initially, I scrolled through the output manually to find the password.

**Explanation:**
- `strings` extracts sequences of printable characters from a file.
- `data.txt` is the file being examined.

## Step 3: Filter the output using grep

To find the relevant line directly, I combined `strings` with `grep`:

```bash
strings data.txt | grep "=="
```

**Explanation:**
- `strings data.txt` extracts human-readable strings.
- `|` (pipe) passes the output to the next command.
- `grep "=="` displays lines containing at least two consecutive equals signs.

This narrowed down the output and helped identify the password without manually scrolling through the entire file.

## Key Takeaways

- Use `strings` to extract readable text from files containing binary or non-text data.
- Use `grep` to search for specific text patterns.
- Use pipes (`|`) to combine commands and filter output efficiently.
- Searching for `==` matches two or more consecutive equals signs, not necessarily exactly two.

## Security Note

Never include passwords or other sensitive credentials in public GitHub write-ups.
