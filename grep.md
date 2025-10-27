# grep Notes

Personal notes and examples on using `grep` to search text inside files and outputs.
---

## 🔍 Basic Usage
```bash
grep "pattern" filename
```
Search for *"pattern"* inside `filename`.

## 🛠️ Common Options
|Option|Descripton|Basic Syntax|
|---|---|---|
|`-A3`|The `grep -A3` command is used to **print the matching line plus 3 lines** ***After*** **it**|`grep -A3 "pattern" filename`|
|`-H`|Show the filename||
|`-i`|Ignore case while matching||
|`-o`|only print the matched part of the line||
|`-r` or `-R`|Recursive search throgh directories||
|`-n`|Show line numbers with matches||
|-v|Invert match(show line *not* matching)||
|-w|Match whole words only||

## Word Boundaries
A word boundary means the "edge" between a word and non-word(space,punctuation, etc).

|Symbol|Meaning|
|---|---|
|`\b`|Word boundary(GNU `grep -P` mode)|
|`\<`|Start of word|
|`\>`|End of word|

## Detect lines with only spaces or tabs
```bash
grep "^[[:space:]]*$" filename
```

## `grep` File-Scope Options
The `--include`, `--exclude`, and `--exclude-dir` options control **which files or directories** `grep` **examines** when using recursive mod (`-r` or `-R`). They are **not filters for matching content,** but **filters for file paths**.

### `--include=GLOB`
This tell `grep` to **only search files** whose names match the given glob pattern (like `*.c`, `*.h`, `file?.txt` etc.).
 * Applies to **file names**, not content.
 * Multiple `--include` options can be given.
#### Syntax:
```bash
grep -r --include="*.c" pattern
```

### `--exclude=GLOB`
This tell `grep` to **skip any file** whose name matches the glob pattern.
 * Works like `--linclude`, but for **excluding** files.
 * Multiple `--exclude` options can be used.

#### Syntax:
```bash
grep -r --exclude="*.log" pattern
```


### `--exclude-dir=GLOB`
This tell `grep` to **skip entire directories** whose names match the given pattern, including their contents.
 * Applies to **directory names** only.
 * Multiple `--exclude-dir` options can be specified.

#### Syntax:
```bash
grep -r --exclude-dir=".git" pattrn
```

#### Searching for Function prototypes
```bash
grep --include="*.h" -rnH '\bsocket.*(int'
```
will display function prototype of `socket` function from all header files recursively from current directory.

### Summary
These are used **with** `-r` **or** `-R` *(recursive grep)*:
|Option|Purpose|Example|
|---|---|---|
|`--include=GLOB`|Only search files matching this pattern|`--include="*.c"`|
|`--exclude=GLOB`|Skip files matching this pattern|`--exclude="*.log"`|
|`--exclude-dir=GLOB`|Skip *directories* matching this pattern|`--exclude-dir=".git"`|

|Option|Meaning|Example|Description|
|---|---|---|---|
|`-A n`|After|`grep -A2 pattern file`|Show `n` lines **after** match|
|`-B n`|Before|`grep -B2 pattern file`|Show `n` lines **before** match|
|`-C n`|Context|`grep -C2 pattern file`|Show `n` lines **before and after** match|
