# vi commands

| Command | Description |
| :-----: | :---------- |
| i | Insert at cursor and goes into cursor mode. |
| a | Write after cursor and goes into insert mode. |
| A | Write at the end of the line and goes into insert mode. |
| ESC | Terminate insert mode. |
| u | Undo last change. |
| U | Undo all changes to the entire line. |
| o | Open at new line and goes into insert mode. |
| dd | Delete current line. |
| 3dd | Delete next three lines. |
| D | Delete contents of the line after the cursor. |
| C | Delete contents of line after the cursor and insert new text. |
| dw | Delete word. |
| 4dw | Delete next four words. |
| cw | Change word. |
| x | Delete character at the cursor. |
| r | Replace character. |
| R | Overwrite character from curor onward. |
| s | Substitute one character under cursor and continue to insert. |
| S | Substitute entire line and begin to insert at the beggining of the line. |
| ~ | Change case of individual character. |
| / | Search for a pattern or word. |

## Moving within a file

| Command | Description |
| :-----: | :---------- |
| k | Move cursor up. |
| j | Move cursor down. |
| h | Move cusor left. |
| l | Move cursor right. |
| G | Move cursor to the end of the file. |

## Saving and closing the file

| Command | Description |
| :-----: | :---------- |
| ZZ | Save the file and quit. |
| :w | Save the file but keep it open. |
| :q | Quit witout saving. |
| :wq | Save the file and quit. |