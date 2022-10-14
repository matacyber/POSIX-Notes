# Part 6: Tools

## Index and Navigate Source Code with ctags
- ctags is an external program that scans through a codebase and generates an index of keywords

### Tip 102 Meet ctags
- Install linux: sudo apt install exuberant-ctags
- Install OSX: brew install ctags
- Use: cd to directory and run `ctags *.{extnesion}`

### Tip 103 Configure Vim to Work with ctags
- `:set tags?` to inspect the defaults
- `:!ctags -R` to invoke ctags from Vim
- An auto command to run ctags every time a file is save
	- `:autocmd BufWritePost * call system("ctags -R")`

### Tip 104 Navigate Keyword Definitions with Vim's Tag Navigation Commands
|Command | Effect|
|---|----|
|`<C-]>` | Jump to the first tag that matches the word under the cursor|
|`g<C-]>`| Prompt user to select from multiple matches for the word under the cursor. If only one match exists, jump to it without prompting.|
|`:tag {keyword}` | Jump to the first tag that matches `{keyword}`|
|`:tjump {keyword}` | Prompt user to select from multiple matches for `{keyword}`. If only one match exists, jump to it without prompting.|
|`:pop` or `<C-t>` | Reverse through tag history|
|`:tag` | Advance through tag history|
|`:tnext` | Jump to next matching tag|
|`:tprev` | Jump to previous matching tag|
|`:tfirst`| Jump to first matching tag|
|`:tlast` | Jump to last matching tag|
|`:tselect` | Prompt user to choose an item from the tag match list|

## Compile Code and Navigate Errors with the Quickfix List

### Tip 106 Browse the Quickfix List

|Command | Action|
|---|----|
|`:cnext` | Jump to next item|
|`:cprev` | Jump to previous item|
|`:cfirst`| Jump to first item|
|`:clast` | Jump to last item|
|`:cnfile`| Jump to first item in next file|
|`:cpfile`| Jump to last item in previous file|
|`:cc N` | Jump to nth item|
|`:copen`| Open the quickfix window|
|`:cclose`| Close the quickfix window|
|`:cdo {cmd}`| Execute {cmd} on each line listed in the quickfix list|
|`:cfdo {cmd}` | Execute {cmd} once for each file listed in the quickfix list|

## Search Project-Wide with grep, vimgrep, and Others
- Vimgrep format: `:vim[grep][!] /{pattern}/[g][j] {file} ...`
- Using `<C-r>/` the history of searches can be searched through

## Dial X for Autocompletion

### Tip 112 Meet Vim's Keyword Autocompletion
|Command | Type of Completion|
|---|----|
|`<C-n>`| Generic Keyword|
|`<C-x><C-n>`| Current buffer keywords|
|`<C-x><C-i>`| Included file keywords|
|`<C-x><C-]>`| tags file keywords|
|`<C-x><C-k>`| Dictionary lookup|
|`<C-x><C-l>`| Whole line completion|
|`<C-x><C-f>`| Filename completion|
|`<C-x><C-o>`| Omni-completion|

### Tip 113 Work with the Autocomplete Pop-Up Menu

|Keystrokes| Effect|
|---|----|
|`<C-n>`| Use the next match form the word list (next match)|
|`<C-p>`| Use the previous match from the word list (previous match)|
|`<Down>`| Select the next match from the word list|
|`<Up>` | Select the previous match from the word list|
|`<C-y>`| Accept the currently selected match (yes)|
|`<C-e>`| Revert the originally typed text (exit from autocompletion)|
|`<C-h> and (<BS>)` | Delete one character from current match|
|`<C-l>` | Add one character from current match|
|`{char}` | Stop completion and insert {char}|

## Find and Fix Typos with Vim's Spell Checker

### Tip 120 Spell Check Your Work
- enable with: `:set spell`

|Command | Effect|
|---|----|
|`]s`| Jump to next spelling error|
|`[s`| Jump to previous spelling error|
|`z=`| Suggest corrections for current word|
|`zg`| Add current word to spell file|
|`zw`| Remove current word from spell file|
|`zug`| Revert `zg` or `zw` command for current word|

### Tip 121 Use Alternate Spelling Dictionaries
- Use `:spelllang={lang}` to switch languages or regions
