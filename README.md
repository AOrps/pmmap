# pmmap
- :brain: Personal Mind Map, aka ramp-up doc on certain functionality

## Search
- Search is done, via a janky tagging system and using grep to find topics

<details>

<Summary> To search for a tag, do: </Summary>


```sh
# The implication that you run this command at the / dir, on a *nix-based OS (or have grep running)

# template 
grep -R '<SEARCH>' . 

# ex
grep -ER '^<!-- tag:.*term.* -->' .
```
</details>

<details>

<Summary> To add a tag, do: </Summary>

```txt
# creating a html comment 
<!-- tag: term1, term2, term3, ...., term_n -->
```
</details>




## :card_file_box: Directory Explanation

```s
.
├── awk                     ; getting *`awk`y
├── bash-buffoonery         ; fun little bash command stuff
├── emacs                   ; emacs shortcuts and how to be more productive
├── oscp                    ; reference guide and (hopefully some explanations)
├── perf                    ; `perf` profiling
├── qemu                    ; qemu commands and tips
└── r2                      ; radare2 

; to update use: `tree -d -L1 --noreport`
```

## :warning: Disclaimer
- Personal Notes on how-to-<tool>, accuracy might not 100% up-to-scruff

---

- [Advanced Github Usage](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams)
- [Gitemojis for commiting](https://gitmoji.dev/)
- [Mermaid Syntax](https://mermaid-js.github.io/mermaid/#/)
