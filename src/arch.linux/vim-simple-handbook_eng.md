# Vi(m) Simple Handbook

> devided by `editor modes`, `normal command`, `more efficiency`, `advanced skills` for progressive learning

## editor modes

- normal mode: default mode, used to mostly operate but not edit file, type `ESC` to switch normal mode from other modes.
- insert mode: edit mode, type `i`/`I`,`a`,`o`/`O` to enter, used for common edit.
- replace mode: type `r`/`R` to enter, used for content replace.
- visual mode: type `v`/`V` to enter, used for code section edit.

## command used in normal mode

- mode switch:
  - type `i`: insert mode, and type `ESC` to return normal mode
- mutiple insert method
  - type `a`: insert after the cursor
  - type `o`: insert new line after current line
  - type `O`: insert new line before current line
  - type `cw`: change the word from current cursor to the end
- moving cursor
  - type `0`: move to the start of current line
  - type `^`: move to the first no-blank character of current line
  - type `$`: move to the end of current line
  - type `g_`: move to the last no-blank character of current line
  - type `/`: search patern results, use `n` for next result
- coyp & paste
  - type `p` OR `P`: paste, `p` for after current line,`P` for before current line
  - type `yy`: copy current line, equal to `ddP`
- Undo & Redo
  - type `u`: undo
  - type `<C-r>: redo
- open, save, quit and change files
  - type `:e`: open a file with path `<path/to/file>`
  - type `:w`: save change to a file, may append a file path
  - type `:saveas`: save as another file with path `<path/to/file>`
  - type `:x`: save and quit, eual to `:wq` and `ZZ`
  - type `:q!`: abort changes and quit. use `:qa!` for all unsaved files
  - type `:bn` and `:bp`: switch next or previous files opened, `:bn` is equal to `:n`
- type `x`: delete character under current cursor
- type `:wq`: save and exit, file name can be appended after `:w`
- type `dd`: delete current line and save it to clipboard
- type `hjkl`: used to replace `←↓↑→`
- type `:help`: query help document

## more efficiency

1. repeat action

- use `.`: repeat previous action once. `N.` to repeat previous action "N" times
- use `N<command>`: repeat specified action "N" times, like this:

```
# delete 2 lines
2dd
# paste text from clipboard after current line 3 times
3p
# insert `desu` 100 times
100idesu [ESC]
```

2. go to anywhere (important!)

- move in the whole file
  - type `NG`: go to "N" line
  - type `gg`: go to the first line
  - type `G`: go to the last line
- move between words
  - type `w`: go to the head of next word
  - type `e`: go to the tail of next word
  - `W` & `E`? the previous move betweend words seemed as variables, while the latter move between words splited by blanks. So, `w` & `e` for programming, and `W` & `E` for articles.
  - type `%`: go to the position paired with `{`, `{`, `[`
  - type `*` & `#`: go to the position paired with current word
  - type `<C+b>` & `<C+f>`: scroll to previous or next screen

3. operate more fastly

- fast copy, delete, toUpper or toLower

```
# copy from line head to line tail
0y$
# copy to last character of current word
ye
# copy characters between `foo`
y2/foo
# delete to line tail
d$
# change letters to uppercase/lowercase untill the line tail
gUe
gue
```

4. visual operation 
use `v`, `V`, `<C-v>` and move cursor to select section, then use operations above.

## Advanced skills: Why vi/vim, not others?

1. cursor inline moving  
with `0`, `^`, `$`, `g_`, `f<?>`/`F`(find), `t<?>`/`T`(till)  

- `0`: move to line head
- `^`: move to first no-blank character of current line
- `$`: move to line tail
- `g_`: move to last no-blank character of current line
- `f<?>`/`F<?>`; move to next/previous position of <?>
- `t<?>`/`T<?>`: move to previous character of `f<?>`/`F<?>`

2. select code section  
use `<action>i<object>` or `<action>a<object>` to select code section.

- action can be any command, like `d`(delete), `y`(copy), `v`(visual select)- object can be any characters, or special letter, like `w`(variable word), `W`(blank spliting word), `s`(a sentence), `p`(a paragraph)

3. section operatoin

```
# batch notes
<C-v><C-d>i-- [ESC]
# <C-v>: visual block mode
# <C-d>: move cursor down(select to next line), can also use `hjkl`
# i: insert mode, when type [ESC], change will be applied to section area lines
```
4. auto completion  
use `<C-n>` or `<C-p>` for auto completion.

5. macro record  

- `qa` to start macro record, and store it to register `a`
- `q` to end macro record
- `N@a` to replay macro stored in register `a` "N" times, `@@` can be also used to replay last macro

```
# begin with a file only containing "1"
# macro demo below, used for number auto increment 100 times till 103:
qaYp<C-a>q
# `qa` to start a macro record
# `Yp` to copy a line after current line
# `<C-a>` to increase 1
# `q` to stop record
@a
@@
100@@
# replay macro stored in register "a", replay last macro once, replay last macro 100 times.
```

6. split screen  

- type `:split`/`: vsplit`: for horizontal/vertical split-screen
- type `<C-w><dir>`: for split-screen switch, `<dir>` may be `hjkl`
- type `<C-w>_`/`<C-w>|`: used to maximize current horizental/vertical split-screen
- type `<C-w>+`/`<C-w>-`: used to increase/decrease size fo current screen
- type `:help split`: used to refer split-screen help document
