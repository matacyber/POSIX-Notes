# Part 1 Modes

- Vim provides a modal user interface

## Normal Mode
This is the entry state for VIM

### Tip 9 - Compose Repeatable Changes
- db - Delete from the cursor's starting position to the beginning of the word.
- b - Move the cursor to the beginning of a word
- dw - From cursor position to the end of the word
- daw - Delete a word

### Tip 10 Use Counts to Do Simple Arithmetic
<C-a> performs addition on numbers
<C-x> performs subtraction on numbers
Putting a number before the command runs the command that many times 
- yyp - Duplicates the line

### Tip 12 Combine and Conquer
- **Operator + Motion = Action**

|Trigger | Effect|
|--------|-------|
| c      | Change|
| d      | Delete|
| y 		 | Yank into register|
| g~ 	   | Swap Case|
| gu 	   | Make lowercase|
| gU 	   | Make uppercase|
| >	  	 | Shift Right|
| <	  	 | Shift Left|
| = 		 | Autoindent|
| ! 	   | Filter {motion} lines through external program|


## Insert Mode
- There are different forms of insert mode that allow us to pull one off commands and things of that nature

### Tip 13 Make Corrections Instantly from Insert Mode
- <C-h> - Delete back one character
- <C-w> - Delete back one word
- <C-u> - Delete back to the start of the line

### Tip 14 Getting back to Normal Mode

|Keystrokes | Effect|
|-----------|-------|
|\<Esc\>	|	Switch to Normal Mode|
|\<C-[\>	|	Switch to Normal Mode|
|\<C-o\>  |		Switch to Insert Normal Mode|
- K - Looks up the Man page for the word under the cursor|
- J - Joins the current and next lines together|

### Tip 15 Paste from the a Register Without Leaving Insert Mode
- \<C-r\>{register} - insert from the register listed
- \<C-r\>\<C-p\>{register} - Insert text literally and fixes any unintended indentation

### Tip 16 Do Back-of-the-Envelope Calculations in Place
- \<C-r\>={Expression}<CR> - Perform the math operation and print it to the screen
Expression register - evaluates a piece of vim script and returns the result

### Tip 17 Insert Unusual Characters by Character Code
- \<C-v\>{code} - Where code is the character code of the character to insert
- ga - Will give the character code of the character under the cusor
- \<C-v\>\<Tab\> - Will always insert a tab

|Keystrokes		|	Effect|
|-------------|-------|
|\<C-v\>{123}  	|	Insert character by decimal code|
|\<C-v\>u{1234}  |      Insert character by hexadecimal code|
|\<C-v\>{nondigit}  |   Insert nondigit literally|
|\<C-k\>{char1}{char2} | Insert character represented by {char1}{char2} digraph|

### Tip 18 Insert Unusal Characters by Digraph
Digraphs are character paris to represent odd characters
:digraphs give a list of digraphs


### Tip 19 Overwriting Existing Text with Replace Mode
\<R\> - Enter replace mode
This overwrites the current character
\<Insert\> - Can toggel between the normal and replace mode
- gR - Enter Virtual Replace mode

## Visual Mode
Allows for blocks/lines of text to defined and operated on

### Tip 20 Grok Visual Mode
- viw - visually select the word
- c - Delete the word and switch to insert mode

### Tip 21 Define a Visual Selection
Visual mode has 3 modes

|Command	|	Effect|
|---|----|
|v	|		Enable character-wise Visual Mode|
|V	|		Enable line-wise Visual mode|
|\<C-v\>	|	Enable block-wise Visual mode|
|gv		|	Reselect the last visual selection|

|Command		|  Effect|
|---|----|
|\<Esc\> / \<C-[\> | Switch to Normal mode|
|v / V / \<C-v\> | Switch to Normal mode (when used from character-, line- or block-wise Visual mode, respectively)|
|v      |       Switch to character-wise Visual mode|
|V		|	  Switch to line-wise Visual mode|
|\<C-v\>   |	  Switch to block-wise Visual mode|
|o	|		  Go to other end of highlighted text|

### Tip 22 Repeat Line-Wise Visual Commands
- \> & \< allow for indenting
- :set shiftwidth=# softtabstop=# expandtab - will define the tab parameters for this action

### Tip 24 Edit Tabular Data with Visual-Block Mode
- \<C-v\> - engage visual block mode
- This mode allows for easy creation of things such as tables and has visual feedback for actions

### Tip 25 Change Columns of Text
- Using visual block mode multiple columns can be changed by highlighting these columns and replacing the text with the "c" command

## Command Line Mode
- This mode comes from VI which comes from EX which is why ex commands exist

### Tip 27 Meet Vim's Command Line
|Command | Effect |
|--------|--------|
|:[range]delete [x] | Delete specified lines [into register x] |
|:[range]yank [x] | Yank specified lines [into register x] |
|:[line]put [x] | Put the text from register x after the specified line |
|:[range]copy {address} | Copy the specified lines to below the line specified by {address}|
|:[range]move {address} | Move the specified lines to below the line specified by {address}|
|:[range]join | Join the specified lines|
|:[range]normal {commands} | Execute Normal mode {commands} on each specified line|
|:[range]substitute/{pattern}/{string}/[flags] | Replace occurrences of {pattern} with {string} on each specified line|
|:[range]global/{pattern}/[cmd] | Execute the Ex command [cmd] on all specified lines where the {pattern} matches|
|:copy | Quick duplicating of lines|
|:edit and :write | Read and write files|
|:tabnew | Create tabs|
|:split |  Split window screen|

### Tip 28 Execute a Command on One or more Consecutive Lines
- . - symbol to represent the current line
- % - all the lines in the current file
- :s or :substitute - replace the occurance of a word with the following word

|Symbol |	Address|
|-------|--------|    
|1		| First line of the file|
|$		| Last line of the file|
|0		| Virtual line above first line of the file|
|.		| Line where the cursor is placed|
|’m		| Line containing mark m|
|’< 	|	Start of visual selection|
|’>	|	End of visual selection|
|% | 		The entire file (shorthand for :1,$)|


### Tip 29 Duplicate or Move Lines using ':t' and ':m' Commands
- :t or :copy - copys the line from one part of the doc to another
- :move - lets us move a line elsewhere in a doc

|Command |	Effect|
|-------|-------|  
|:6t.	| Copy line 6 to just below the current line|
|:t6	|	Copy the current line to just below line 6|
|:t.	|	Duplicate the current line (similar to Normal mode yyp)|
|:t$	|	Copy the current line to the end of the file|
|:’<,’>t0 | Copy the visually selected lines to the start of the file|

### Tip 31 Repeat the Last Ex Command
- @: - repeats the last ex command
- bn: - will step forward through commands
- bp: - will step backward through commands
- @@ - repeats the last @: command

### Tip 34 Recall Commands from history
|Command |	Action|
|--------|--------|  
|q/	|	Open the command-line window with history of searches|
|q:	|	Open the command-line window with history of Ex commands|
|ctrl-f	| Switch from Command-Line mode to the command-line window|

### Tip 35 Run Command in the Shell
|Command	 | Effect|
|----------|-------| 
|:shell  	 |		Start a shell (return to Vim by typing exit)|
|:!{cmd} 	 |	Execute {cmd} with the shell|
|:read !{cmd} 	|		Execute {cmd} in the shell and insert its standard output below the cursor|
|:[range]write !{cmd} |	Execute {cmd} in the shell with [range] lines as standard input|
|:[range]!{filter} 	|	Filter the specified [range] through external program {filter}|

### Tip 36 Run Multiple Ex Commands as a Batch
- .vim files can be written and sourced in vim to run multiple commands
- :args can grab individual args to run
- :argdo will run the arg

