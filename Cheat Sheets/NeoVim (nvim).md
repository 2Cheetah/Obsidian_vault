# NeoVim (nvim)
**Neovim is a text editor with plugins which make it as powerful as IDE.**
[Link to GitHub](https://github.com/neovim/neovim)
[Видео от Диджитализируй - # БОЖЕСТВЕННЫЙ nvim как IDE для Python, Rust и всех-всех-всех — встречаем LSP!](https://youtu.be/PA7zZNJXJEk)

## Installation
- Ubuntu
```bash
sudo apt install neovim
```
- Manjaro Linux
```shell
sudo pacman -Syu neovim
```

## Configuration
Configuration file can be stored in:
```
~/.config/nvim/init.vim
```
[Sample configuration file](https://github.com/2Cheetah/Obsidian_vault/blob/main/init.vim)

## Plugins
- [vim-plug](https://github.com/junegunn/vim-plug)
- [Conquer of Completion - Coc](https://github.com/neoclide/coc.nvim)
	- Requires nodejs
- Static type checker for Python by Microsoft. [Pyright](https://github.com/microsoft/pyright). Can be installed with [coc-pyright](https://github.com/fannheyward/coc-pyright)

## Navigation and usage
`h` - left `j` - down `k` - up `l` - right
`0` - move to the beginning of the line
`$` - move to the end of the line
`:q!` - exit without saving
`:wq` - exit with saving


`x` - delete the character under the cursor

`i` - insert the text before the cursor
`A` - append the text (insert the text in the end of the line)
`a` - append the text after the cursor position
`o` - insert line and go to the insert mode
`O` - insert line before the cursor position and enters the Insert mode

`dw` - delete word from the cursor position till the end of the word
`d$` - delete from the cursor position till the end of the line
`d0` - delete from the cursor position till the beginning of the line
`d[operator]`
Operators:
- `w` - until the start of the next word
- `e` - to the end of the current word
- `$` - to the end of the line
- `0` - to the beginning of the line

`[number]d[operator]`
number:
1, 2, ..., etc - how many times the operation will be carried out
e.g:
`2w` - move cursor two words forward
`3e` - move cursor to the end of the third word forward

`dd` - delete the whole line
`2dd` - delete two lines

`u` - undo command
`U` - fix the whole line
`Ctrl+r <C-r>` - repeat command

`p` - paste previously deleted or copied text after the cursor
`P` - paste before the cursor
`y` - copy selected text. Can be used with operators, e.g. yw or even y4w

`rx` - replace the character at the cursor with x
`R` - Replace mode

`c` - change operator
`ce` - change until the end of the word. Deletes everything from the cursor position till the end of the word and enters insert mode
`c$` - change until the end of the line

`<C-g>` - show location in a file and the file status
`gg` - go to the beginning of the file
`G` - go to the end of the file
`[number]G` - go to the \[number\] line

`/[phrase]` - followed by a phrase to search for the phrase
`?[phrase]` - followed by a phrase to search for the phrase but backwards
`n` - next entry
`N` - previous entry

`<C-o>` - to go back where you came from
`<C-i>` - to go forward

`%` - to find matching ), ] or }

`:s/old/new/g` - to substitute "new" for "old". Where flag "g" means to replace globally in the whole line

`:#,#s/old/new/g` - where # are the line numbers of the range of lines where the substitution is to be done (i.e., 1,3 means from line 1 to line 3, inclusive)

`:%s/old/new/g` - to change every occurence in the whole file

`:%s/old/new/gc` - to change every in the whole file, with a prompt whether to substitute or not

`:!` followed by an external command to execute that command
e.g. `:!ls` or `:!rm`

`v` - visual selection. Further can be saved with the command `:'<,'>w [FILENAME]` or deleted with `d` or something else

`:r [FILENAME]` - retrieves text from the file
or
e.g. `:r !ls` - retrieves output of the `ls` command

`<C-w><C-w>` - switch from one window to another