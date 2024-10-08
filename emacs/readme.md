# emacs

| Hotkey | Key
| :----: | :-----
| `C`    | Control
| `M`    | ALT
| `^`    | Shift

## Top Tier Productivity Packages
| Package | Reason
| :------ | :------
| eglot   | client lsp
| company | auto-complete


## Shortcuts

### Vanilla
- Emacs

| Shortcut | Functionality
| :----:   | :-----
| `C-a`    | Jump to the beginning of the line (^)
| `C-e`    | Jump to the end of the line ($)
| `C-k`    | Cut at that point
| `C-g`    | Cancel command
| `C-s`    | search for text
| `C-x o`  | Switch between screens (windows)
| `C-- C-x o`  | Switch between screens (windows) but the other way
| `C-x 2`  | Vertical Split screens (windows)
| `C-x 3`  | Horizontal Split screens (windows)
| `C-x 0`  | Exit screens (windows)
| `M-^1` or `M-!` | Shell command
| `M-x` | Emacs Command Invoker
| `M-/` | Dabbrev-expand: Naive word completion
| `C-x b` | change buffer (small line)
| `C-x C-b` | Change buffer (show menu in new buffer)
| `C-x u` | Undo
| `C-w`   | Destructive copy to clipboard
| `M-w`   | Non-destructive Copy to clipboard
| `C-y`   | Paste from Clipboard
| `C-x-i` | Insert from file
| `C-v`   | Scroll down (page)
| `M-v`   | Scroll  up  (page)

- To do the opposite of some commands try to do `C--`, this works to 'negate' commands

- Within, emacs `term`, `(M-X) term`:
  - `C-c C-j`: line run (can switch between things) but can't use sysints or delete without mucking about
  - `C-c C-k`: char run (can't switch between things) but can use sysints (^C, ^L, ...) and delete

- Within, emacs `query-replace`, `(M-X) query-replace`:
  - `C-q C-j`: newline

- Within i-search, `C-s`:
  - `C-s`: go to the end of next match
  - `C-r`: go to the start of the previous match

### Bonusz
- Other Packages

| Shortcut | Package | Functionality |
| :----:   | :-----: | :--------
| `C-M-i`  | eglot   | Completion-at-point (tries to autofill code)
| `C-n`    | company | Next selection at auto-complete scroll
| `C-p`    | company | Previous selection at auto-complete scroll
    
## Commands

| Functions | Description 
| :------:  | :------
| `(local-set-key KEY COMMAND)` | Binds a key to a local keymap used by the active buffer
| `(describe-keymap ...)` | check existing keybinds
| `(term ...)` | open terminal in emacs
| `(list-packages)` | search available packages for emacs
| `(man ...)` | get man pages
| `(doctor ...)` | talk to a psychotherapist in emacs
| `(query-replace ...)` | looks for all instances of <QUERY> then iteratively goes thru each instance for replacement  
| `(compile ...)` | custom build from emacs
| `(erc ...) ` | irc in emacs


## Melpa

### Installation 
```lisp
;; .emacs | init.el
(require 'package)
(add-to-list 'package-archives '("melpa-stable" . "https://stable.melpa.org/packages/") t)
(package-initialize)
```

```elisp
M-x package-refresh-contents
```


### reference
- https://melpa.org/#/getting-started



## Changing Dired to display by type

### Manual
- after pressing: `C-u s`, type `-alS` (based on `ls`)


### reference:
- https://stackoverflow.com/questions/27378909/how-to-sort-files-in-emacs-dired
