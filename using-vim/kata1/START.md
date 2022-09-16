# Kata 1

> If you have done this kata before you can probably skip to the last line of this document.

This kata will teach you the basics of using VIM. By practicing it multiple times you commit the motions to memory and improve your speed.

It is intended to be executed from beginning to end. This will result in the contents being the same as they were to start with. If you mess up, you can always run `git reset`.

## Prerequisites

For this kata `vim` (or `vi`) is required. This comes by default on most Mac OSX and most Linux distributions. If you are on Windows I suggest using the WSL. If you like you can install [vim](https://www.vim.org/) or [Neovim](https://neovim.io/). In later katas I will be using Neovim so I suggest that.

## Contents

1. Navigating folders and files
2. Moving inside of files
3. Copying content to memory
4. Editing files effectively

## Getting started

This kata is learned much like I have learned martial arts katas in the past. You batch a few moves together until you have the full kata. Once you have got the batch of moves down, you move onto the next batch. This will be slightly different as we will complete the full kata every time. This is because the kata is designed that once all steps are complete, the project will be in the same state it started in. We could of course use git to reset but I like how this setup just flows.

So lets get started. On your command line, make sure the directory is set to the same one this *START.md* file is in, and execute the following.

> Tip: If at any point you get stuck, you can quit VIM by hitting ESC and then `:q!`

`vim 1-navigating-folders-files/a/a-instructions.md`