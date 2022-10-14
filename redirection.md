# Redirection

- File descriptors: stdin, stdout, stderr (0,1,2)
- `>` redirect stdout to a file
- `>>` append stdout to a file
- redirect will overwrite the file
- `<` redirect stdin to a file
- `<<` append stdin to a file
- `2>` redirect stderr to a file
- command 2> /dev/null - redirect stderr to /dev/null (don't print the output)
- `|` redirect stdout of one command to the stdin to another
