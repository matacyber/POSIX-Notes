# Part 5: Patterns

## Matching Patterns and Literals

### Tip 73 Tune the Case Sensitivity of Search Patterns
- Search can be set case insensitive with `:set ignorecase`
- `\c` searchs without case sensitivity
- `\C` searchs with case sensitivity
- smartcase can be used to try and guess the case sensitivity

|Pattern | 'ignorecase' | 'smartcase' | Matches|
|---|---|---|----|
|foo | off | - | foo|
|foo | on | - | foo Foo FOO|
|foo | on | on | foo Foo FOO|
|Foo | on | on | Foo|
|Foo | on | off | foo Foo FOO|
|`\cfoo` | - | - | foo Foo FOO|
|`foo\C` | - | - | foo|

### Tip 74 Use the \v Pattern Switch for Regex Searches
- This options assumes that all characters have special meaning except `"_"`, uppercase, lowercase, and 0-9

## Search

### Tip 80 Meet the Search Command

|Command | Effect|
|---|----|
|`n` | Jump to next match, preserving direction and offset|
|`N` | Jump to previous match, preserving direction and offset|
|`/<CR>` | Jump forward to next match of same pattern|
|`?<CR>` | Jump backward to previous match of same pattern|
|`gn` | Enable character-wise Visual mode and select next search match|
|`gN` | Enable character-wise Visual mode and select previous search match|

### Tip 82 Preview the First Match Before Execution
- `incsearch` option allows for the match to be previewed and updated while typing it

### Tip 84 Operate on a Complete Search Match
- `gU{motion}` convert a range of text to uppercase
- `dgn` delete the matching text
- `cgn{word}<Esc>` repalce each match with the word

## Substitution

### Tip 88 Meet the Substitute Command
- `:[range]s[ubstitute]/{pattern}/{string}/[flags]` is the common format
- The g flag make the substitute command act globally
- The c flag give the oppurtunity to confirm or reject each change
- The n flag suppresses the usual substitute behavior, causing the command to report the number of occurrences that would be affected if we ran the command
- The & flag tells VIM to reuse the last flag

|Symbol | Represents|
|---|----|
|`\r` | Insert carriage return|
|`\t` | Insert a tab character|
|`\\` | Insert a single backlash|
|`\1` | Insert the first submatch|
|`\2` | Insert the second submatch (and so on, up to `\9`)|
|`\0` | Insert the entire matched pattern|
|`&` | Insert the entire matched pattern|
|`~` | Use {string} from the previous invocation of :substitute|
|`\={Vim Script}` | Evaluate {Vim Script} expression; use result as replacement {string}|

### Tip 91 Eyeball Each Substitution

|Trigger | Effect|
|---|----|
|`y` | Substitute this match|
|`n` | Skip this match|
|`q` | Quit substituting|
|`l` | "last" - Substitute this match, then quit|
|`a` | "all" - Substitute this and any remaining matches|
|`<C-e>` | Scroll the screen up|
|`<C-y>` | Scroll the screen down|

## Global Commands

### Tip 98 Meet the Global Command
- `:[range] global[!] /{pattern}/ [cmd]` is the command form for this command
- Lines can be deleted with a search pattern then `:g//d` basically, using `:g/re/d`
