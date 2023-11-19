# R (Programming Language)

## Command line tools:
- `R` 
  - Start R interactively
- `Rscript`
  - Run a `<prog-name>.R` file

## Package Management

- Within R, you can do the following:
```R
; install package 'corrplot'
install.packages('corrplot')

; remove package 'corrplot'
remove.packages('corrplot')

```

- There seems to be no official way of listing R dependencies, but some work has been done on this topic: https://stackoverflow.com/questions/38838191/r-equivalent-of-pip-freeze-how-to-install-all-r-dependencies-from-a-file-list
