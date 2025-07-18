# Shell Globbing and Regular Expression

## Terminology
|Term|Meaning|
|---|---|
|Globbing|Pattern matching used by the **shell** (e.g., `bash`) to expand filenames|
|Regex|Formal language used for **text pattern matching**, used by `grep`, `sed`, `awk`, et.|
|Wildcard|General term often referring to ***glob characcters*** like (`*`), it is not related with ***regex***|

## Shell Globbing
 * Where it appears:
   * `ls`, `cp`, `mv`, etc.
   * Bash script
   * File path expansion (e.g., `*.c`)

### Core Globbing patterns
|Pattern|Meaning|Example|
|---|---|---|
|`*`|Matches *zero or more characters*| `*.txt` matches `a.txt`, `abc.txt`|
|`?`|Matches *exactly one character*|`?.txt` matches `a.txt`, but not `ab.txt`|
|`[abc]`|Maches *one characters* from the set|`file[123]` matches `file1`, `file2`, `file3`|
|`[a-z]`|Matches any character in range|`file[a-z].txt`|
|`^[abc]`|Matches anything *except* these|`[^0-9]` not a digit|
|`{a,b,c}`|Matches any of the comma-separated values|`{a,b}.txt` $\rightarrow$ `a.txt`, `b.txt`|

#### Globbing Pitfalls
 * Globs *do not* understand regex syntax like `+`, `|`, `()` - they'll be treated literally.
 * `[a-z]` is safe, but locale can affect range (`LC_COLLATE`)
 * Brace expansion (`{}`) is **not pattern matching** - it's **string generation** (done before globbing)

## Learn Regular Expressions (Regex)
 * Where it appear:
   * `grep`, `egrep`, `sed`, `awk`, `perl`, etc.
   * Programming Language (`Python`, 'C`, `JavaScript`, etc.)
   * `find` with `-regex` or `-iregex`
### Major Regex Flavors in Linux:
|Tool|Regex Flavor|
|---|---|
|`grep`|Basic Regular Expression (BRE) by default|
|`egrep`, `grep -E`|Extended Regular Expression (ERE)|
|`sed`|Basic Regular Expression|
|`awk`|Extended Regular Expression|
|`perl`|Perl Compatible Regular Expression (PCRE)|

#### Regex Metacharacters
|Pattern|Meaning|BRE or ERE|
|---|---|---|
|`.`|Any one character|Both|
|`*`|Zero or more of previous|Both|
|`+`|One or more (in ERE)|ERE only|
|`?`|Zero or one (in ERE)|ERE only|
|`^`|Beginning of line|Both|
|`$`|End of line|Both|
|`[]`|Character class|Both|
|`[^]`|Negated class|Both|
|`\{n,m\}`|Quantifier (BRE needs `\`)|BRE|
|`{n,m}`|Quantifer|ERE|
|`|`|Alteration|
|`()`|Grouping|BRE requires `\(` and `\)`|
