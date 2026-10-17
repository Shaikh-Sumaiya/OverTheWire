# Bandit Level 11 → Level 12

## Objective
The password for the next level is stored in `data.txt` and is encoded using ROT13.

## Step 1: Log in as bandit11

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

## Step 2: View the file

```bash
cat data.txt
```

The output contains text encoded using ROT13, where each letter is shifted by 13 positions in the alphabet.

## Step 3: Decode the ROT13 text

```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### How it works

- `cat data.txt` displays the contents of the file.
- `|` passes the output of the first command to the next command.
- `tr` translates characters according to the mapping provided.
- `'A-Za-z'` represents uppercase A–Z and lowercase a–z.
- `'N-ZA-Mn-za-m'` defines the replacement sequence for uppercase and lowercase letters, shifting each letter by 13 positions and wrapping around the alphabet.

The decoded output reveals the password for the next level.

## Key Takeaways

- ROT13 is a letter-substitution technique that shifts each letter by 13 positions.
- The `tr` command can translate characters using specified character sets.
- The pipe (`|`) passes one command's output as input to another command.

## Security Note

ROT13 is not encryption. It is a simple substitution technique that provides no real security because anyone can reverse it without a key.
