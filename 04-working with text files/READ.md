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

## Displaying File Contents with 'head' and 'tail' 

'head' and 'tail' display specific portions of text files.

### Basic Commands

| Command | Purpose |
| --- | --- |
| 'head FILE' | First 10 lines by default |
| 'tail FILE; | Last 10 lines by default |
| 'head -n 5 FILE' | First 5 lines |
| 'tail -n 5 FILE' | Last 5 lines |
| 'tail -f FILE' | Will show the last 10 lines following newly appended lines |

### Specifying Lines

The '-n' option specifies the number of lines. 

'''bash
head -n 5 /etc/passwd
tail -n 5 /etc/passwd
'''

Current versions also support 'tail -5 as shorthand for 'tail -n 5'.

### Monitoring Log Files

'''bash
sudo tail -f /var/log/messages
'''

'-f' follows the file and displays new lines as they are appended. This is useful for troubleshooting system logs. 

Press 'Ctrl+C' to stop monitoring.

### Combining 'head' and 'tail'

Display only line 11 of 'etc/passwd':

'''bash
head -n 11 /etc/passwd | tail -n 1
'''

1. 'head' outputs lines 1-11.
2. The pipe passes that output to 'tail'.
3. 'tail -n 1' displays only line 11.

### Key Takeaways

- 'head' = beginning of a file
- 'tail' = end of a file
- '-n' = number of lines
- '-f' = follow new lines
- 'Ctrl+C' = stop monitoring
- Pipes combine commands to select specific lines


## Filtering and Sorting Text

### 1. The cut command

The cut command extracts specific fields or columns from text

It is useful when working with structured files such as /etc/passwd

Important options: 
- -d = Defines the delimited (character separating fields)
- -f = Specifies which field(s) to extract

Example: 

'''Bash
cut -d ':' -f 1 /etc/passwd
'''

Explanation:
- -d ':' tells Linux that fields are separated by colons
- -f 1 selects the first field
- /etc/passwd is the file being processed

  This command displays usernames because the first field in /etc/passwd contains the usernmae

  To extract multiple fields:

  '''Bash
  cut -d ':' -f 1,3 /etc/passwd
  '''

  This displays usernames and their user IDs (UIDs)

### 2. The sort Command

The sort command arranges lines of text into a specified order

By default, sorting is lexicographic, which means numbers are not necessarily sorted by their numerical value 

Important options:
* -n = Sort numerically
