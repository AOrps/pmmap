# emacs

| Hotkey | Key
| :----: | :-----
| `C`    | Control
| `M`    | ALT
| `^`    | Shift

## Shortcuts

### Vanilla
- Emacs

| Shortcut | Functionality
| :----:   | :-----
| `C-g`    | Cancel command
| `C-x o`  | Switch between screens (windows)
| `C-- C-x o`  | Switch between screens (windows) but the other way
| `C-x 2`  | Vertical Split screens (windows)
| `C-x 3`  | Horizontal Split screens (windows)
| `C-x 0`  | Exit screens (windows)
| `M-^1` or `M-!` | Shell command
| `M-x` | Emacs Command Invoker

- To do the opposite of some commands try to do `C--`, this works to 'negate' commands

- Within, emacs `term`, `(M-X) term`:
  - `C-c j`: line run (can switch between things) but can't use sysints or delete without mucking about
  - `C-c k`: char run (can't switch between things) but can use sysints (^C, ^L, ...) and delete


### Bonusz
- Other Packages

| Shortcut | Package | Functionality |
| :----:   | :-----: | :--------
| `C-M-i`  | eglot   | Completion-at-point (tries to autofill code)

    
## Commands

| Functions | Description 
| :------:  | :------
| `(local-set-key KEY COMMAND)` | Binds a key to a local keymap used by the active buffer
| `(describe-keymap ...)` | check existing keybinds
| `(term ...)` | open terminal in emacs
