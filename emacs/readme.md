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
| `C-x 2`  | Vertical Split screens (windows)
| `C-x 3`  | Horizontal Split screens (windows)
| `C-x 0`  | Exit screens (windows)
| `M-^1` or `M-!` | Shell command
| `M-x` | Emacs Command Invoker


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
