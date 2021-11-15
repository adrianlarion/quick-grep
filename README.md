# Quick Grep

### Search for match in file
`grep hello file`

### Search for a match in multiple files
`grep hello file1 file2`


### Search for match in all files in current dir (will show a warning if dirs are present too)
`grep hello *`

### Search for match in all files in current dir. Suppress warning if dirs are present. (it searches for 'hello' in all files. 'skip' is an action passed to '-d')
`grep -d skip hello *`


### Case insensitive
`grep -i hello file` 

### Invert search
`grep -v hello file`

### Match whole words. Will match ' year ' but not 'goodyear'
`grep -w year file`

### Match whole lines. Will match 'year' (where 'year' is the single word on a line. Won't match 'one year', 'goodyear'.
`grep -x year file`

### Treat the search pattern literally, not as a regex. Will match the literal '[Yy]ear' but won't match 'year'.
`grep -F '[Yy]ear' file`

### Search for multiple patterns. Match both 'year' and 'hello'.
`grep -e hello -e year file`

### Read search patterns from a file. Each pattern on a new line. Match all found patterns.
`grep -f patterns.txt file`


### Count matching lines for pattern (NOT matching patterns). Display a number - how many lines matched. 
`grep -c hello file`


### Print file names where match found (don't print the actual matches).
`grep -l hello *.txt`


### Print file names where match NOT found.
`grep -L hello *.txt`


### Search for pattern only whithin the first Nth lines. (only in the first 10 lines in the example)
`grep -m 10 hello file`


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

### Also print N trailing lines AFTER matched line. (N lines AFTER the matched line)
`grep -A 2 year file`

### Also print N trailing lines BEFORE matched line. (N lines BEFORE the matched line)
`grep -B 2 year file`

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


### Seach recursively in dir. If simlynk encountered, follow it and search the file pointed by the symlink. 
`grep -R hello`
