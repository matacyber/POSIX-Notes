# Part 2 Files 

## Manage Multiple Files
- VIM allows for the user to manage multiple files at the same time
- This is done with the use of buffer list

### Tip 37 Track Open Files with the Buffer List
- The buffer is the in-memory representation of a file
- Working with the buffer can be through :write, :update, and :saveas
- `:ls` will show all the open buffers
- `'bnext` will move to the next buffer
- /% indicates the buffer that is current visable
- /# resprents an alternate file
- /<C-^/> can switch between the buffers
- `:bprev` move back through the buffers
- `:bnext` move forward through the buffers
- `:bfirst` move to the first buffer
- `:blast` move to the last buffer
- `:buffer {buffername}` switch to that buffer
- `:bufdo` run an Ex command on all buffers
- `:bdelete` delete the given buffer

### Tip 38 Group Buffers into a Collection with the Argument List
- The arguments list can be populated when commands are run with :args
- * matches all characters
- `**` matches all characters recurvise down into directories and sub-directories

### Tip 39 Manage Hidden Files
| Command|	Effect|
|---|----|
| :w[rite]| Write the contents of the buffer to disk|
| :e[dit]!| Read the file from disk back into the buffer (that is, revert changes)|
|:qa[ll]!| Close all windows, discarding changes without warning|
| :wa[ll]| Write all modified buffers to disk|

### Tip 40 Divide Your Workspace
- `/<C-w/>s` spilts the window horizontally
- `/<C-w/>v` split the window vertically
- :split will accomplish the same thing

|Command |	Effect|
|---|----|
|:w[rite] | Write the contents of the buffer to disk|
|:e[dit]! | Read the file from disk back into the buffer (that is, revert changes)|
|:qa[ll]! | Close all windows, discarding changes without warning|
|:wa[ll] | Write all modified buffers to disk|

|Command | 	Effect|
|---|----|
|<C-w>w | Cycle between open windows|
|<C-w>h | Focus the window to the left|
|<C-w>j | Focus the window below|
|<C-w>k | Focus the window above|
|<C-w>l | Focus the window to the right|

|Ex Command	| Normal Command	| Effect|
|---|----|----|
|:clo[se]  |<C-w>c | Close the active window|
|:on[ly] | <C-w>o | Keep only the active window, closing all others|

|Keystrokes	| Buffer Contents|
|---|----|
|<C-w>= | Equalize width and height of all windows|
|<C-w>_ | Maximize height of the active window|
|`<C-w>|` | Maximize width of the active window|
|[N]<C-w>_ | Set active window height to [N] rows|
|`[N]<C-w>|` |  Set active window width to [N] columns|

### Tip 41 Organize Your Window Layouts with Tab Pages
|Command |	Effect|
|---|----|
|:tabe[dit] {filename} | Open {filename} in a new tab|
|<C-w>T | Move the current window into its own tab|
|:tabc[lose] | Close the current tab page and all of its windows|
|:tabo[nly] | Keep the active tab page, closing all others|

|Ex Command	| Normal Command |	Effect|
|---|----|----|
|:tabn[ext] {N} | {N}gt | Switch to tab page number {N}|
|:tabn[ext] | gt | Switch to the next tab page|
|:tabp[revious] | gT | Switch to the previous tab page|
