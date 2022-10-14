# Part 3 Getting Around Faster
## Navigate Inside Files with Motions
### Tip 48 Distinguish Between Real Lines and Display Lines
- The wrap setting allows for lines to wrap and be easier to see
- 'number' setting will give line numbers to see around this
- `j` and `k` will move by real lines
- `gj` and `gk` will move by diplay lines

|Command | Move Cursor|
|----|----|
|`j` | Down one real line|
|`gj` | Down one display line|
|`k` | Up one real line| 
|`gk` | Up one display line| 
|`0` | First character on a real line|
|`g0` | First character on a display line|
|`^` | First nonblank character of a real line|
|`g^` | First nonblank character of a display line|
|`$` | End of a real line|
|`g$` | End of a display line|

### Tip 49 Move Word-Wise

|Command | Move Cursor|
|---|-----|
|`w` | Forward to start of next word|
|`b` | Backward to start of current/previous word|
|`e` | Forward to end of current/next word|
|`ge` | Backward to end of previous word|

- words - any sequence character as a sequence of nonblank characters separated with whitespace
- WORDS - a sequence of nonblank characters separated with whitespace

### Tip 50 Find by character
- `f{char}` - seacrch for the first occurance of a character and go to it
- `;` will move forward when searching by character

### Tip 51 Search to Navigate
- Lines can be deleted with `d{motion}`
	- `d/{chars}` delete from the start to the first occurance of that pattern

### Tip 52 Trace Your Selection with Precision Text Objects

|Text| Object Selction|
|---|----|
|`a)` or `ab` | A pair of ()|
|`a}` or `aB` | A pair of {}|
|`a]`| A pair of []|
|`a>`| A pair of <>|
|`a'`| A pair of ''|
|`a"`| A pair of ""|
|`at`| A pair of <xml></xml>|
|`i)`| or `ib` Inside of ()|
|`i}`| or `iB` Inside of {}|
|`i]`| Inside of []|
|`i>`| Inside of <>|
|`i'`| Inside of ''|
|`i"`| Inside of ""|
|`it`| Inside of <xml></xml>|

- `c{motion}` Change motion - delete section and change to insert mode

### Tip 53 Delete Around, or Change Inside

|Keystrokes Current...|
|---|----|
|`iw` | word|
|`iW` | WORD|
|`is` | sentence|
|`ip` | paragraph|
|`aw` | word + space(s)|
|`aW` | WORD + space(s)|
|`as` | sentence + space(s)|
|`ap` | paragraph + blank line(s)|

- `d{motion}` tends to work well with `aw`, `as`, and `ap`
- `c{motion}` tends to work well with `iw` and similar

### Tip 54 Mark Your Place and Snap Back to it
- `m{a-zA-Z}` marks the current cursor location with a designated letter
- lowercase marks are local to the buffer
- uppercase marks are global
- `'{mark}` jumps to the mark and the whitespace next to it
- `(backtick){mark}` jumps to exact point were the mark was set
- 26 marks can be set per buffer

## Navigate Between Files With Jumps

|Command | Effect|
|---|----|
|`[count]G`| Jump to line #|
|`/pattern<CR>`/`?pattern<CR>`/`n`/`N` | Jump to next/previous occurance of pattern|
|`%` | Jump to matching parenthesis|
|`(`/`)` | Jump to the start of previous/next sentence|
|`{`/`}` | Jump to the start of the previous/next paragraph|
|`H`/`M`/`L` | Jump to the top/middle/bottom of the screen|
|`gf` | Jump to file name under the cursor|
|`<C-]>` | Jump to definition of keyword under the cursor|
|`(backtick){mark}`/`(backtick){mark}` | Jump to a mark|

### Tip 59 Snap Between Files Using Global Marks
- `m{letter}` create a mark at the current cursor postion
- `:grep` Uses grep with in the buffer
- `:vimgrep` Uses a form of grep bulitin to VIM
- `:make` Runs make in the current VIM session
