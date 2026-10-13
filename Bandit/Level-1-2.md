# Bandit Level 1 → Level 2

## Objective
Retrieve the password for the next level from a file named `-`.

## Concepts Learned
- Reading files with unusual filenames
- Using relative paths in Linux
- Understanding special command-line arguments

## Steps Performed

### 1. Listed the files

```bash
ls
```

The output showed a file named `-`.

### 2. Read the file

```bash
cat ./-
```

The `./` prefix specifies the current directory, allowing the command to treat `-` as a filename rather than as a special argument.

## Key Takeaways
- `cat` displays the contents of a file.
- `./` explicitly refers to the current directory.
- Filenames that resemble command options or special arguments may require a different path or syntax.

## Security Note
The password has been excluded from this write-up.
