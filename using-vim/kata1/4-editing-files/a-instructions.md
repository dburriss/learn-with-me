# Editing files (1/3)

As mentioned before, Vim is about more than typing characters. It is about manipulating documents.  
So far we have used NORMAL mode and COMMAND mode. First we will use INSERT mode for inserting characters. Then we will make use of VISUAL and VISUAL LINE mode for selecting text.

## Instructions

We are going to use the Example text below to create a new file.

> Tip: You can always use `u` in NORMAL mode to undo a change in a buffer.

### Creating the heading

1. Type command `:vsplit 4-editing-files/text.md`. text.md does not exist but now we have a buffer open for it.
2. The new window should have focus but you can use `Ctrl+w, w` to toggle to the new *text.md* file if needed. You can make sure you are on the correct buffer by using the `:ls` command. The buffer that is currently active will have a %a while the other visible buffer (these instructions) will have a #a.
3. Press `i` to enter INSERT mode. Type the following: "# The case for nuclear energy". Press ENTER twice for 2 newlines.
4. Press ESC to exit INSERT mode.
5. Let's actually create the file on the filesystem now. Run the command `:w` to write the buffer to the file text.md.

### Copying the first paragraph

6. Toggle so you are on the buffer containing these instructions. In NORMAL mode move the cursor to the beginning of the paragraph starting with "Nuclear energy has a bad reputation" (line 46 Hint: `46gg` will get you there fast).
7. Now enter VISUAL mode by pressing `v`. We can use any of the usual movement keys to select the paragraph. The easiest is probably to press `}` (`Shift+]`) to move to the end of the paragraph.
8. Press `y` for yank. This is VIM's version of copy where it saves it in a register for later use.
9. Use the motion `Ctrl+w,w` to move to the text.md window and push `p` (for paste) it on line 3 of text.md.

### Copying the heading 2

10. Return to this buffer using `Ctrl+w,w` (or however else you would like) and place the cursor on the line with the title "Deaths by fuel source per 1000 terra watt hours"
11. Use the motion `yy` to copy the line. It is good to know it will copy newlines as well so expect some extra whitespace.
12. Use motion `Ctrl+w,w` to change to the text.md buffer and paste it under the paragraph that was pasted in the previous section.

### Copying the list

13. Return to this buffer using `Ctrl+w,w` and position the cursor at the start of the first line of the list of fuel source deaths.
14. Press `Shift+V` to enter VISUAL LINE mode which makes for easy selection of whole lines.
15. Use the movement key `j` to move down until all items in the list are highlighted. Then press `y`.
16. Flip over to text.md using `Shift+w,w` and paste the list after the heading using `p`.

> There are other ways to select ranges and we could of course have done this in one go. This is for practice though...

17. Return to this buffer using `Ctrl+w,w` and then switch the buffer using command `:e 4-editing-files/b-instructions.md`

# Example:

Nuclear energy has a bad reputation but until we have better batteries it remains the cleanest way to guarantee consistant energy. But is it safe?

# Deaths by fuel source per 1000 terra watt hours

- Coal : 100000
- Cold fusion : 0
- Hydro : 1400
- Natural gas : 4000
- Nuclear : 90
- Oil : 36000
- Rooftop solar : 440
- Wind : 150
