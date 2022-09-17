# Navigating folders and files (2/3)

You just used another mode. VIM enters COMMAND mode when you type `:`.
We have seen how we can open `vim path/to/file` and how we can use the command `:Ex` to launch netrw and navigate the filesystem to a file.

# Instructions

> Tip: You can append ! behind a command to force it. For example `:e! file.txt` will load in file.txt even if you have pending changes (you will lose your changes).

Next we will enter a command now to jump directly to a file. Recall that we launched VIM in the *kata1* folder, so relative paths are from there.

1. `:edit 1-navigating-folders-files/c-instructions.md`

> Tip 1: You can use `:e` as a shorthand command for `:edit`

> Tip 2: You can see what the root folder you are operating from by executing the command `:pwd` (print working directory)
