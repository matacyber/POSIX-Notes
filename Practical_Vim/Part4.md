# Part 4 Registers

## Copy and Paste
- `p` pastes from the unnamed register
- `ddp` cuts a line then places it elsewhere
- `yyp` duplicates the current line to the next line
- `diw` cuts the word into the unnamed register
- `yiw` copys the current word into the unnamed register
- `"{register}` specify which register to use 
- `"0` references the yank register
- `"0P` will paste from the yank register
- `:reg` will list the contents of the registers
- registers are listed `"a-"z`
- `"_` is the black hole register where nothing is returned (i.e. deleted fully)
- `"+p` will paste from an external application
- `"+` references the system clipboard
- `"+` The X11 clipboard, used with cut, copy, and paste
- `"*` The X11 primary, used with middle mouse button
- `"=` is the expression register where vim script can be run

|Register | Contents|
|---|----|
|`"%` | Name of the current file|
|`"#` | Name of the alternate file|
|`".` | Last inserted text|
|`":` | Last Ex command|
|`"/` | Last search pattern|

## Macros
- `q` is the key for recording macros
- `@@` execute the most recent macro
- `@{register}` execute the macro from that register
- Macros will execute until no more characters matching the macro are found (when running multiple time)
- `q{Capital}` will append to that register
- `wall` will save all files in the buffer
- `:put {register}` will paste it into a document
- Then it can be edited and added back to the register with `"{register}dd`
