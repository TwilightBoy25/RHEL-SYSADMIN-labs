# Working With Text Files

## Using Common Text File-Related Tools

Below are commands that can display text files in an efficient way.

| Command | Explanation |
| --- | --- |
| less | Opens the text file in a pager, which allows for easy reading |
| cat | Dumps the contents of the text file on the screen |
| head | Shows the top of the text file |
| tail | Shows the bottom of the text file |
| cut | Used to filter specific columns or characters from a text file |
| sort | Sorts the contents of a text file | 
| wc | Counts the number of lines, words, and characters in a text file |

### Viewing Files with 'less'

'less' is useful for reading longer text files because it allows navigation and searching without modifying the file.

'''bash
less /etc/passwd
'''

Use controls while inside 'less':

| Key | Action |
| --- | --- |
| '/text' | Search forward for text |
| '?text' | Search backward for text |
| 'n' | Repeat previous search |
| 'G' | Jump to the end |
| 'q' | Quit 'less' |

### Using 'less' with Pipes

Command output can be piped into 'less':

'''bash
ps aux | less 
'''

The pipe sends the standard output of 'ps aux' to the standard input of 'less'.

'''text
ps aux -> STDOUT -> | STDIN -> less
'''

'ps aux' displays a detailed list of running processes. For this section, the important concept is using ' | less' to make long command output easier to browse.

### Viewing Files with 'cat'

'cat' displays the contents of a file directly in the terminal:

'''bash
cat /etc/passwd
'''

'cat' is convenient for short files. For longer files, 'less' is usually easier because it provides navigation and searching. 

### Quick Mental Model

'''text
cat -> show me everything
less -> let me browse this
head -> show me the beginning
tail -> show me the end
cut -> give me specific parts
sort -> put this in order
wc -> count this
'''

### 'less' vs 'cat' 

'''text
Short file / quick output -> cat
Long file / need navigation -> less
'''

