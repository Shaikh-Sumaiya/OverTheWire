# Bandit Level 10 → Level 11

## Objective

Find the password for the next level in `data.txt`. The file contains Base64-encoded data.

## Step 1: Log in as bandit10

Connect to the Bandit server using SSH:

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

## Step 2: Inspect the file

```bash
cat data.txt
```

The output looked like a string of letters and numbers and ended with `==`, which suggested that it might be Base64-encoded data.

**Note:** The `=` character can be used as padding in Base64, but its presence alone does not confirm that text is Base64-encoded.

## Step 3: Decode the data

```bash
base64 -d data.txt
```

**Explanation:**

- `base64` runs the Base64 utility.
- `-d` tells the utility to decode the data.
- `data.txt` is the file containing the encoded text.

The decoded output revealed the password for the next level.

## Key Takeaways

- Base64 is an encoding format, not encryption.
- Use `cat` to inspect a file's contents.
- Use `base64 -d` to decode Base64-encoded data.
- The `=` character can indicate Base64 padding, but it is not definitive proof of Base64 encoding.

## Security Note

Never include passwords or other sensitive credentials in public GitHub write-ups.
