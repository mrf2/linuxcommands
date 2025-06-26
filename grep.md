# grep Notes

Personal notes and examples on using `grep` to search text inside files and outputs.
---

## 🔍 Basic Usage
```bash
grep "pattern" filename
```
Search for *"pattern"* inside `filename`.

## 🛠️ Common Options
|Option|Descripton|
|---|---|
|`-H`|Show the filename|
|`-i`|Ignore case while matching|
|`-o`|only print the matched part of the line|
|`-r` or `-R`|Recursive search throgh directories|
|`-n`|Show line numbers with matches|
|-v|Invert match(show line *not* matching)|
|-w|Match whole words only|

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

