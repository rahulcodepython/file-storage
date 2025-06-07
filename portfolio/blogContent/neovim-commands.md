---
title: Neovim Commands
description: This is a blog contains some useful and common neovim commands.
date: 03/18/2025
---

Here is a **comprehensive list** of **important NeoVim keybindings**, covering **navigation, editing, search, buffers, splits, macros, registers, and more**.

---

## **📝 Basic Movements**

| Keybinding | Action                                            |
| ---------- | ------------------------------------------------- |
| `h`        | Move left                                         |
| `l`        | Move right                                        |
| `j`        | Move down                                         |
| `k`        | Move up                                           |
| `0`        | Move to the beginning of the line                 |
| `^`        | Move to the first non-blank character of the line |
| `$`        | Move to the end of the line                       |
| `gg`       | Move to the beginning of the file                 |
| `G`        | Move to the end of the file                       |
| `5G`       | Move to line 5 (replace 5 with any number)        |
| `H`        | Move to the top of the screen                     |
| `M`        | Move to the middle of the screen                  |
| `L`        | Move to the bottom of the screen                  |
| `zz`       | Center the current line on the screen             |

---

## **📜 Scrolling**

| Keybinding | Action                  |
| ---------- | ----------------------- |
| `Ctrl + d` | Scroll down half a page |
| `Ctrl + u` | Scroll up half a page   |
| `Ctrl + f` | Scroll down a full page |
| `Ctrl + b` | Scroll up a full page   |

---

## **🔍 Searching**

| Keybinding       | Action                                                  |
| ---------------- | ------------------------------------------------------- |
| `/text`          | Search forward for "text"                               |
| `?text`          | Search backward for "text"                              |
| `n`              | Repeat last search (forward)                            |
| `N`              | Repeat last search (backward)                           |
| `*`              | Search for the word under the cursor (forward)          |
| `#`              | Search for the word under the cursor (backward)         |
| `:%s/old/new/g`  | Replace all occurrences of "old" with "new" in the file |
| `:%s/old/new/gc` | Replace with confirmation                               |
| `:noh`           | Remove search highlight                                 |

---

## **✂️ Editing**

| Keybinding | Action                                        |
| ---------- | --------------------------------------------- |
| `i`        | Insert mode before cursor                     |
| `I`        | Insert at the beginning of the line           |
| `a`        | Insert mode after cursor                      |
| `A`        | Insert mode at the end of the line            |
| `o`        | Insert a new line below and enter insert mode |
| `O`        | Insert a new line above and enter insert mode |
| `r`        | Replace a single character                    |
| `R`        | Enter replace mode                            |
| `J`        | Join the current line with the next one       |
| `u`        | Undo last change                              |
| `Ctrl + r` | Redo last undone change                       |
| `.`        | Repeat the last command                       |

---

## **📑 Copy, Cut, and Paste (Yank, Delete, Put)**

| Keybinding | Action                                |
| ---------- | ------------------------------------- |
| `yy`       | Yank (copy) the current line          |
| `y$`       | Yank from cursor to end of the line   |
| `yw`       | Yank one word                         |
| `p`        | Paste after cursor                    |
| `P`        | Paste before cursor                   |
| `dd`       | Delete (cut) the current line         |
| `dw`       | Delete a word                         |
| `d$`       | Delete from cursor to end of the line |
| `x`        | Delete (cut) a single character       |

---

## **📌 Visual Mode**

| Keybinding | Action                                     |
| ---------- | ------------------------------------------ |
| `v`        | Enter visual mode (character selection)    |
| `V`        | Enter visual line mode                     |
| `Ctrl + v` | Enter visual block mode (column selection) |
| `y`        | Yank selection                             |
| `d`        | Delete selection                           |
| `>`        | Indent right                               |
| `<`        | Indent left                                |

---

## **📂 Buffers & Tabs**

| Keybinding       | Action                      |
| ---------------- | --------------------------- |
| `:e <file>`      | Open a file                 |
| `:bnext` (`:bn`) | Move to the next buffer     |
| `:bprev` (`:bp`) | Move to the previous buffer |
| `:bd`            | Close the current buffer    |
| `:buffers`       | Show open buffers           |
| `:tabnew <file>` | Open a file in a new tab    |
| `gt`             | Switch to the next tab      |
| `gT`             | Switch to the previous tab  |

---

## **🖥️ Windows (Splits)**

| Keybinding         | Action                        |
| ------------------ | ----------------------------- |
| `:split` or `:sp`  | Split the window horizontally |
| `:vsplit` or `:vs` | Split the window vertically   |
| `Ctrl + w + w`     | Switch between windows        |
| `Ctrl + w + h`     | Move to the left split        |
| `Ctrl + w + l`     | Move to the right split       |
| `Ctrl + w + j`     | Move to the lower split       |
| `Ctrl + w + k`     | Move to the upper split       |
| `Ctrl + w + q`     | Close the current split       |
| `Ctrl + w + o`     | Close all other splits        |

---

## **📜 Marks and Jumps**

| Keybinding  | Action                                   |
| ----------- | ---------------------------------------- |
| `m<letter>` | Set a mark at the current position       |
| `'<letter>` | Jump to a mark within the same file      |
| ``          | Jump back to the last cursor position    |
| `Ctrl + o`  | Jump to the previous cursor position     |
| `Ctrl + i`  | Jump forward to the next cursor position |

---

## **⏺️ Macros**

| Keybinding  | Action                                         |
| ----------- | ---------------------------------------------- |
| `q<letter>` | Start recording a macro in register `<letter>` |
| `q`         | Stop recording a macro                         |
| `@<letter>` | Play the recorded macro                        |
| `@@`        | Repeat the last macro                          |

---

## **📒 Registers (Clipboard & Yank History)**

| Keybinding   | Action                  |
| ------------ | ----------------------- |
| `"aY`        | Yank into register "a"  |
| `"ap`        | Paste from register "a" |
| `:registers` | Show all registers      |

---

## **🚀 Miscellaneous**

| Keybinding        | Action                                     |
| ----------------- | ------------------------------------------ |
| `:w`              | Save file                                  |
| `:q`              | Quit NeoVim                                |
| `:q!`             | Quit without saving                        |
| `:wq` or `ZZ`     | Save and quit                              |
| `:x`              | Save and quit (only if changes were made)  |
| `:help <command>` | Show help for a command                    |
| `Ctrl + g`        | Show file name and cursor position         |
| `ga`              | Show ASCII value of character under cursor |

---

## **💡 Useful Custom Mappings**

To customize mappings, add these to your **`~/.config/nvim/init.vim` or `init.lua`**:

```vim
" Map space as leader key
let mapleader=" "

" Save file with leader + w
nnoremap <leader>w :w<CR>

" Quit NeoVim with leader + q
nnoremap <leader>q :q<CR>

" Copy to system clipboard
nnoremap <leader>y "+y
vnoremap <leader>y "+y

" Paste from system clipboard
nnoremap <leader>p "+p
```

---

## **🎯 Conclusion**

These keybindings **cover almost everything you need** to efficiently navigate and edit in NeoVim. 🚀 If you want more details, check out the official documentation with:

```sh
:help
```

Happy Vimming! 🎉 😃
