# Quick Grep
* Quick grep one-liner reference and tutorial. Combine these simple options into longer ones as needed.

----

### Search for match (the string 'hello') in file (called generically 'file'). Display every line that matches pattern (in this case every line containing 'hello')
`grep hello file`

### Search for match in file and use quotes on the pattern. Not required unless you have special chars that are expanded by the shell. (in this case not required)
`grep 'hello' file`

### Search for a match in multiple files
`grep hello file1 file2`

### Search for match in all files in current dir (will show a warning if dirs are present too)
`grep hello *`

### Search for a match in all files in curent dir. Don't show errors if dirs are present. (grep treats dirs just as ordinary files and tries to "read" them). '-s' is for silent. Will also skip errors regarding nonexistent files.
`grep -s hello *`

### Search for a match in all files than end with '.py'
`grep hello *.py`

### Search for match in all files in current dir. Suppress warning if dirs are present. (it searches for 'hello' in all files. 'skip' is an action passed to '-d'). Show warnings about unexisting files.
`grep -d skip hello *`


### Case insensitive
`grep -i Hello file` 

### Invert search
`grep -v hello file`

### Combine options. Case insensitive AND invert search
`grep -iv Hello file`


### Use regex. (search for either 'year' or 'Year')
`grep '[Yy]ear' file`


### Use basic regex (default). Match literal 'years+' in string. ('?+{|()' have no special meaning). Don't match 'years', 'yearss', 'yearsss', etc.
`grep 'years+' file`

### Use extendend regex. Match 'years', 'yearss', 'yearsss', etc. ('+' means one or more of the chars before it, in this case an 's'). '?+{|()' have special meaning.
`grep -E 'years+' file`

### Same as above (extended regex)
`egrep 'years+' file`


### Match whole words. Will match ' year ' but not 'goodyear'
`grep -w year file`

### Match whole lines. Will match 'year' (where 'year' is the single word on a line. Won't match 'one year', 'goodyear'.
`grep -x year file`

### Treat the search pattern literally, not as a regex. Will match the literal '[Yy]ear' but won't match 'year'.
`grep -F '[Yy]ear' file`

### Search for multiple patterns. Match both 'year' and 'hello'.
`grep -e hello -e year file`

### Read search patterns from a file. Each pattern on a new line. Match all found patterns. 'patterns.txt' can have 'word' on one line, '[Yy]ear' on the second, etc.
`grep -f patterns.txt file`

### Read search patterns from file AND from text passed to option '-e'. Match all found patterns.
`grep -f patterns.txt -e '[Ee]xtra' file`


### Count matching lines for pattern (NOT matching patterns). Display a number - how many lines matched. 
`grep -c hello file`

### Count matching lines for every file except dirs (supressed with '-s'). Display how mayn lines matched (for every file). Will show multiple files with 0 or more matches. 
`grep -sc hello *`


### Print ONLY file names where match found (don't print the actual matches).
`grep -l hello *.txt`


### Print ONLY file names where match NOT found.
`grep -L hello *.txt`


### Search for pattern only whithin the first Nth lines. (only in the first 10 lines in the example)
`grep -m 10 hello file`

### Search for pattern whithin Nth lines for every file in current dir. Skip dirs. Note how we concatenate '-m' and '10'. We could've alse written them with a space, like '-m 10'
`grep -sm10 hello *`


### Print only the matched parts, without the surrounding text. Example will print 'year', 'Year', 'YEAR', etc - each an a new line
`grep -o [Yy]ear file`


### Supress error messages about files not existing.
`grep -s hello file nonexisting_file`

### Print filename before each match. Eg: 'file:goodyear' (default when multiple files are searched).
`grep -H year file`


### Supress printing filenames before each match (even if multiple files are searched)
`grep -h year file file2`

### Add line number before each output line (Eg: '1:goodyear')
`grep -n year file`

### Print both line number and file name (eg: 'file:3:goodyear'). '-H' will force to display filename even if just one file (by default not shown). '-s' suppress dir missing warns.
`grep -nHs year *`

### Also print N trailing lines AFTER matched line. (show N lines AFTER the matched line)
`grep -A 2 year file`

### Also print N trailing lines BEFORE matched line. (show N lines BEFORE the matched line)
`grep -B 2 year file`

### Print 2 lines before and 4 lines after matched line.
`grep -B2 -A4 hello file`


### Also print N lines BEFORE and N lines AFTER matched line (eg: 2 before and 2 after)
`grep -C 2 year file`

### Force process binary files. Without this you'll get 'grep: /usr/bin/pamon: binary file matches'. (search for string 'au' in binary file)
`grep -a au /usr/bin/pamon`

### Exclude files that match this pattern. (eg: don't search .py or .c files)
`grep --exclude=*.py --exclude=*.c year *`

### Include files that match this pattern. Use in conjuction with --exclude. (exclude all .py files and then include only 'main.py' in the search)
`grep --exclude=*.py --include=main.py year *`


### Search recursively in dir (go as deep as possible, searching for files). DON'T follow symlinks. No warning about searching dirs shown.
`grep -r hello`

### Exclude dirs from searching. Useful when using '-r' to skip certain dirs, such as '.git'
`grep hello -r --exclude-dir='.git'`

### Seach recursively in dir. If simlynk encountered, follow it and search the file pointed by the symlink. 
`grep -R hello`

### Print total byte count before matched lines. First line (from file, not matched line) has a count of '0'. Eg: line 1 - '0:abc', line 2 '4:def'. It shows 4 because it has counted 4 bytes until now ('abc' + newline from the first file)
`grep -b hello file`

### Search for 'hello' in files that might start with the '-' character. Without the '--' a file like '-myfile' won't be searched. WARNING - having such a file in your dir will BREAK "normal" grep functioning (eg: `grep hello *` WON'T SHOW all 'hello' lines from files. Reason is that when it encounters file '-x' it treats it as an option since it expands the `*` wildcard)
`grep -- hello *`

### Sausage options 1. Search in binary files (text too but friendly toward binaries). Print byte count (or offset as grep calls it), force filename, ignorecase, show match only, also show line count, search recursively in this dir. Output is like 'hau/f:15:193:hello'
` grep -abHionr hello`.



