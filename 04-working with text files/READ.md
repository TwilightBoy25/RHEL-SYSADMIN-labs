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
