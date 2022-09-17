# Moving inside of files (1/3)

In NORMAL mode you can quickly fly around text files. We have looked at opening files, now we will look at moving around within a file. In Vim, these keys we use to move the cursor are called motions (or jump motions more specifically).

## Instructions

1. Type the following command to enable line numbers: `:set number`.
2. Use the `j` key to move down to instruction 3 (the line after this line).
3. Use the `l` key to move to the end of this line. Go down 1 line with `j`.
4. Use the `h` key to get to the beginning of this line.
5. Go to point number 1 (line 7) of the instructions using the `k` key.
6. Type the following: `13gg`. This will take you to the final instruction (point 7).
7. Head to the next kata moves using the command: `:e +200 2-moving-inside-files/b-instructions.md`

> Tip: When opening a file from command line or an `edit` command you can use `+<line-number>` to jump to a specific line number. Only `+` with no number would place the cursor on the last line of the file eg `:e + path/to/file`.
