# Editing files (1/3)

Hopefully this far in you can see that we stayed in NORMAL mode for a lot of that, dipping into INSERT, VISUAL, and VISUAL LINE mode as we needed to. In this sequence we will continue to manipulate the text.md buffer so you should have this buffer and that buffer open in some sort of split screen (horizontal or vertical).

## Instructions

We will be sorting the list in order of highest mortality rate to lowest.

> Tip 1: You should still have line numbers but if you closed Vim you can use  `:set number` to get them back.

1. Using `Ctrl+w,w` ensure that you have the text.md buffer focused.
2. Delete Cold fusion. Navigate down to the 2nd list item "Cold fusion" and use the motion `dd`.
3. Copy paste Oil to second place. Move to "Oil" line and press `dd`, then move to "Coal" and press `p`.
4. Swap "Hydro" and "Natural gas". Move down one using `j` so cursor is on "Hydro". Run command `:m .+1` to move the current line down 1 line.
5. Now we could move "Rooftop solar" and "Wind" to line before "Nuclear"'s line number (`:13,14m 11` where 12 is my line number for "Nuclear") OR an easier command in this case is to move "Nuclear" to the end of the file using command `:12m$`. You can use `u` for undo to try both moves.
6. Write your changes to text.md by running command `:w`.

> Tip 2: The format for move is `:[range]m[ove] {address}` so the spaces are optional and if no range is given then the current line is assumed. `.` is for current line and `$` is for the last line.

7. Return to this buffer using `Ctrl+w,w` and then switch the buffer using command `:e 4-editing-files/c-instructions.md`