# grep and find - My Notes and Daily use

These are my running notes while exploring how `grep` and `find` work under the hood and how I can use them effectively in daily tasks.

---
## grep - Searching for text inside files
- Basic:
  ```bash
  grep "searching-text" file-name

- Recursive:
  ```bash
  grep -r "searching-text" /search/path

- Case-insensitive + filter by extension
  ```bash
  grep -ri --include="*.c" "main"

## find - Locating files by conditions
- Basic syntax:
  ```bash
  find <start_path> <conditions> <action>
- Find all *.log* files under *`/var`*:
  ```bash
  find /var -type f -name "*.log"
- Find `.c` and `.h` files:
  ```bash
  find /usr -type f \( -name "*.c" -o -name "*.h" \)

## Using find with grep (Powerful combo)
- Search for all `.conf` files containing ***Listen***:
  ```bash
  find /etc -type f -name "*.conf" -exec grep -iH "Listen" {} \;

## Personal Learnings
>- I often forget escaping parentheses `\(<space> -o <space>\)` in find - now I remember: `\( <space> \)`
>- `exec grep -iH ...` lets me keep the filename in the output while ignoring case-sensitivity
>- These tools help me explore unknown systems and configs deeply


